pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {

            steps{

                script{
                    withSonarQubeEnv(credentialsId : 'sonar-token') { 
                     sh "mvn sonar:sonar"
                    }
                   timeout(time: 1, unit: 'HOURS') {
                     def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                         error "Pipeline aborted due to quality gate failure: ${qg.status}"
                       }
                   }

                   sh "mvn clean install"
                   sh 'pwd'
                   sh 'ls'
                }


            }
        }

       

     













        // stage('Test') {
        //     steps {
        //         sh 'mvn test -Dmaven.test.failure.ignore=true'
        //     }
        //     post {
        //         success {
        //             junit 'target/surefire-reports/*.xml'
        //         }
        //     }
        // }
        // stage('Deliver') {
        //     steps {
        //         sh './jenkins/scripts/deliver.sh'
        //     }
        // }
    }
}



