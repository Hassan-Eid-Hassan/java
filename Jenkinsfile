pipeline {
    agent {
            label 'jenkins-slave1'
}
    stages {
        stage('GIT') {
            steps {
                 git 'https://github.com/Hassan-Eid-Hassan/java.git'
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
        //stage('Deploy'){
        //    steps {
        //        sh """ ssh root@${Cluster} 'kubectl set image deployment java-deployment java=hassaneid/java:${version}' """
      //      }
    //    }
        stage('mail'){
            steps {
            emailext body: 'test', recipientProviders: [buildUser()], subject: 'test', to: 'hassaneid339@gmail.com'
            }
        }
    }
}
