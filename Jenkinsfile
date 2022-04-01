pipeline{
    agent any
    stages{


        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }



        stage("sonar quality check"){


            agent{
                docker{
                    image 'openjdk:11'
                }
            }
            steps{
                script{

                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                     // some block
                    }

                }
            }
        }   
    }
    post{
        always{
            echo "success"
        }
        
    }
}