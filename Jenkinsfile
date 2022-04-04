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
                    sh 'docker build -t 34.125.158.228:8083/firstapp:${VERSION} .'
                }
            }
           
        }
        stage ('Push docker image'){

            steps{
                script{
                         withCredentials([string(credentialsId: 'docker-secret-auth', variable: 'dockersecrettoken')]) {

                        sh '''

                        docker login -u soamibm -p ${dockersecrettoken} 34.125.158.228:8083

                        docker push 34.125.158.228:8083/firstapp:${VERSION}

                        '''
                        
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
    // post{success {
        //             junit 'target/surefire-reports/*.xml'
        //         }
            
    //     }
    // }
}



