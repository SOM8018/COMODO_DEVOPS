pipeline {
    agent any 
    // {
    //     docker {
    //         image 'maven'
    //         args '-v $HOME/.m2:/root/.m2'
    //     }
    // }
    tools {
        maven 'MAVEN'
    }
    
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Check Sonarqube qualitygate') {

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
        stage ('Build'){

            steps{
                //i will first build the docker image and push it to docker hub for testing purpose then i will go for nexus repo
                // script{
                //     docker build . -t 
                // }
                sh 'pwd'

            }
        }
        stage ('Sent a email if build successful'){

            steps{
                sh 'pwd'
                

            }
        }
        stage ('Deploy '){

            steps{
                sh 'pwd'
                

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



