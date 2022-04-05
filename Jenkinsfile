pipeline {
    agent any 
    // {
    //     docker {
    //         image 'maven'
    //         args '-v $HOME/.m2:/root/.m2'
    //     }
    // }
    environment{
        VERSION="${env.BUILD_ID}"
    }
    tools {
        maven 'MAVEN'
    }
    
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Check Sonarqube qualitygate') {

            steps{
                      //First i will check with sonarqube quality gates , if it will pass then it will build
                      // otherwise it will show the error
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
        stage ('Build') {

            steps{
                //i will first build the docker image and push it to docker hub for testing purpose then i will go for nexus repo
                // script{
                //     docker build . -t 
                // }
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '455b6a62-bbad-46ae-bb82-95437cba744c', url: 'https://github.com/SOM8018/COMODO_DEVOPS.git']]])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage ('Build Docker image'){

            //Building jar: /var/lib/jenkins/workspace/devops_Test/target/my-app-1.0-SNAPSHOT.jar

            steps{
                script{
                    //sh 'docker build -t soamfirstdockerimage/my-app-1.0 . '
                    sh 'docker build -t 34.125.158.228:8083/firstapp:${VERSION} .'   //for nexus
                    sh 'docker build -t soamibm/firstapp:${VERSION} .'    //for docker
                }
            }
           
        }
        stage ('Push docker image to Nexus repo'){

            steps{
                script{
                       withCredentials([string(credentialsId: 'nexus-docker-password', variable: 'nexus-docker-auth')]) {

                        //34.125.158.228:8083 is the nexus repo ip 
                        sh '''
                          
                        docker login -u admin -p Nexus@123 34.125.158.228:8083

                        docker push 34.125.158.228:8083/firstapp:${VERSION}

                        docker rmi 34.125.158.228:8083/firstapp:${VERSION}

                        '''

                    }                   
                    
                }
                
                

            } 
        }
        stage ('Push docker image to docker hub'){

            steps{
                script{
                       withCredentials([string(credentialsId: 'nexus-docker-password', variable: 'nexus-docker-auth')]) {

                        //docker push soamibm/firstapp:tagname
                        sh '''
                          
                        docker login -u soamibm -p T#lstraibm12345 

                        docker push soamibm/firstapp:${VERSION}

                        docker rmi soamibm/firstapp:${VERSION}
                        '''

                    }                   
                    
                }
                
                

            } 
        }
        stage ('Deploy to Kubernetes Cluster'){

            steps{
                
               sshagent(['ssh-master1-kubernetes']) {

                   sh "scp -o StringHostKeyChecking=no Deployment.yaml ubuntu@34.125.209.59:/home/ubuntu"

                   script{

                       try{

                           sh "ssh ubuntu@34.125.209.59 kubectl apply -f ."

                       }catch(error){
                           "ssh ubuntu@34.125.209.59 kubectl apply -f ."
                       }
                   }
    
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
    post{
            always{
                mail bcc: '', body: "<br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "${currentBuild.result} CI: Project name -> ${env.JOB_NAME}", to: "mesomofficial@gmail.com" ; 
            }
        }
}



