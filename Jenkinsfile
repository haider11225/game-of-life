pipeline{
    tools{
        jdk 'jdk852'
        maven 'maven381'
    }
    agent none
    stages{
        stage('Compile'){
            agent{label 'linux_slave02'}
            steps{
                sh 'mvn compile'
                }
        }
        stage('test'){
            agent{label 'linux_slave02'}
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
            agent{label 'linux_slave02'}
            steps{
                sh 'mvn package'
            }
        }
        stage('Deploy'){
            agent{label 'master'}
            steps{
                git 'https://github.com/vpractice/game-of-life.git'
                sh '''
                    rm -rf jenkins-dimages
                    mkdir jenkins-dimages
                    cd jenkins-dimages
                    cp /var/lib/jenkins/workspace/GOL-CICDPipeline/gameoflife-web/target/gameoflife.war .
                    touch dockerfile
                    echo "From tomcat" >> dockerfile
                    echo "ADD gameoflife.war /usr/local/tomcat/webapps" >> dockerfile
                    echo CMD '"catalina.sh"' '"run"' >> dockerfile
                    echo "EXPOSE 8080" >> dockerfile
                    sudo docker build -t golimage2:$BUILD_NUMBER .
                    sudo docker run -itd -P golimage2:$BUILD_NUMBER
                    '''
            }
        }
    }
}
