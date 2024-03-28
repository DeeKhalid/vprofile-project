pipeline {
    agent any 
    tools {
        maven "Maven3"
        jdk "OracleJDK8"
    }
     
    environment {
        SNAP_REPO = 'khalidpro-snapshort'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'khalidpro-release'
        CENTRAL_REPO = 'khalidpro-maven-central'
        NEXUSIP      = '172.31.23.9'
        NEXUSPORT    = '8081'
        NEXUS_GRP_REPO = 'khalidpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
        SONARSERVER = 'sonarserver'
        SONARSCANNER = 'sonarscanner'

    }
         
    stages {
        stage('Build'){
            steps {
                script {
                    // Set enviroment variable for Maven build
                    env.MAVEN_OPTS = "-Dmaven.repo.local=$WORKSPACE/.m2/repository"
                    // Execute Maven build                
                    sh 'mvn -s settings.xml -DskipTests install'
                }
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Test'){
            steps {
                sh 'mvn -s settings.xml test'
            }    
            
            
        }
        stage('Checkstyle Analysis'){
            steps {
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }
        stage('Sonar Analysis') {
            evniroment{
                scannerHome = tools "${SONARSCANNER}"
            }
            steps {
                withSonarQubeEnv("${SONARSERVER}") {
                   sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=khalidpro \
                   -Dsonar.projectName=khalidpro \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
              
   
                }
            }
        }
    }
}  

