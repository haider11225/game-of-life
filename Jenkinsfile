pipeline{
    tools{
        jdk 'myjdk'
        maven 'mymaven'
    }
    agent none
    stages{
        stage('Checkout'){
            agent any
            steps{
                git 'https://github.com/vpractice/game-of-life.git'
            }
        }
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
        stage('Package'){
            agent {label 'Win_Node'}
            steps{
                git 'https://github.com/vpractice/game-of-life.git'
                bat 'mvn package'
            }
        }
    }
}
