pipeline {
    agent any
    stages {
        stage('Update pom') {
            steps {
                sh 'echo upd pom'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy To Maven') {
            steps {
                sh 'echo deploy'
            }
        }
        stage('ArchiveArtifacts') {
            steps {
                archiveArtifacts artifacts: 'target/TestJinweb.war', fingerprint: true, onlyIfSuccessful: true
            }
        }
        stage('Build DockerImage') {
            steps {
                sh 'service docker start'
                sh 'cd target && touch Dockerfile'
                sh 'echo FROM tomcat:9.0.22 >> target/Dockerfile'
                sh 'echo LABEL maintainer="hzk" >> target/Dockerfile'
                sh 'echo RUN rm -f /usr/local/tomcat/README.md >> target/Dockerfile'
                sh 'echo RUN rm -f /usr/local/tomcat/BUILDING.txt >> target/Dockerfile'
                sh 'echo RUN rm -f /usr/local/tomcat/CONTRIBUTING.md >> target/Dockerfile'
                sh 'echo RUN rm -rf /usr/local/tomcat/webapps/ROOT >> target/Dockerfile'
                sh 'echo RUN rm -rf /usr/local/tomcat/webapps/docs >> target/Dockerfile'
                sh 'echo RUN rm -rf /usr/local/tomcat/webapps/examples >> target/Dockerfile'
                sh 'echo RUN rm -rf /usr/local/tomcat/webapps/host-manager >> target/Dockerfile'
                sh 'echo RUN rm -rf /usr/local/tomcat/webapps/manager >> target/Dockerfile'
                sh 'cd target && docker build -t registry.hzkvm.com/library/testjinweb:1.0 .'
            }
        }
    }
}