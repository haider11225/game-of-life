pipeline{
    tools{
        jdk 'mymaven'
        maven 'mymaven'
    }
    agent none
    stages{
        stage('Compile'){
            agent any
            steps{
                sh 'mvn compile'
            }
        }
        stage('Test'){
            agent any
            steps{
                sh 'mvn test'
            }
            post{
                always{
                    junit 'gameoflife-web/target/surefire-reports/*.xml'
                }
            }
        }
        stage('Packae'){
            agent any
            steps{
                sh 'mvn package'
            }
        }
    }
}
