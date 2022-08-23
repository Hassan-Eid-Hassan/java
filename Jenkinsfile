pipeline {
    agent any
    stages {
        stage('GIT') {
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/khalednoh/demo1.git'
                echo 'test 3'
            }
        }
        stage('Build JAR') {
            steps {
                  sh "mvn clean test package install"
            }
        }
        stage('Artifacts JAR') {
            steps {
                 archiveArtifacts artifacts: 'target/*.jar'
                 archiveArtifacts artifacts: 'target/classes/com/example/*'
            }
        }
        stage('Build Image'){
            steps {
                sh "docker build -t hassaneid/java:${BUILD_NUMBER} ."
            }
                
        }
        //stage('Scan') {
          //  steps {
          //      sh "docker scan hassaneid/java:${BUILD_NUMBER} >> scanresult.txt | set +e"
        //
        //    }
        //}
        stage('Publish') {
            steps {
               sh 'docker push hassaneid/java:${BUILD_NUMBER}'
            }
        }
        stage('Deploy'){
            steps {
                sh """ ssh -i /home/ec2-user/eand.pem ec2-user@52.91.25.97 'sudo kubectl set image deployment java-deployment java=hassaneid/java:${BUILD_NUMBER}' """
            } 
        }

    }
}
