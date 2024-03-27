pipeline {
    agent any 
    tools {
        maven "Maven3"
        jdk "OracleJDK11"
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

    }
         
    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
        }
    }
}  

