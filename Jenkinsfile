pipeline{
    tools{
        jdk 'jdk852'
        maven 'maven381'
    }
    agent none
    stages{
        stage('Compile'){
            agent{label 'centos83'}
            steps{
                git 'https://github.com/vpractice/game-of-life.git'
                sh 'mvn compile'
            }
        }
        stage('Test'){
            agent{label 'master'}
            steps{
                git 'https://github.com/vpractice/game-of-life.git'
                sh 'mvn test'
            }
        }
        stage('Package'){
            agent{label 'win2k16slave'}
            steps{
                git 'https://github.com/vpractice/game-of-life.git'
                bat 'mvn package'
            }
        }
        stage('Deploy'){
            agent{label 'master'}
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
