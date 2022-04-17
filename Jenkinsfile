pipeline{
    tools{
        jdk 'jdk8u152'
        maven 'maven385'
    }
    agent none
    stages{
        stage('Compile'){
            agent any
            steps{
                git 'https://github.com/vpractice/game-of-life.git'
                sh 'mvn compile'
            }
        }
        stage('Test'){
            agent any
            steps{
                git 'https://github.com/vpractice/game-of-life.git'
                sh 'mvn test'
            }
        }
        stage('Package'){
            agent any
            steps{
                git 'https://github.com/vpractice/game-of-life.git'
                sh 'mvn package'
            }
        }
        stage('Deploy'){
            agent any
            steps{
                git 'https://github.com/vpractice/game-of-life.git'
                sh '''rm -rf jenkins-dimages
                mkdir jenkins-dimages
                cd jenkins-dimages
                cp /var/lib/jenkins/workspace/GOL-CICDPipeline/gameoflife-web/target/gameoflife.war .
                echo "From tomcat" >> dockerfile
                echo "ADD gameoflife.war /usr/local/tomcat/webapps" >> dockerfile
                echo CMD '"catalina.sh"' '"run"' >> dockerfile
                echo "EXPOSE 8080" >> dockerfile
                sudo docker build -t golimagenew:$BUILD_NUMBER .
                sudo docker run -itd -P golimagenew:$BUILD_NUMBER'''
            }
        }
        
    }
}
