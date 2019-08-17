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
        stage('Send Artifacts') {
            steps {
              sh 'scp target/TestJinweb.war root@192.168.2.136:/root/dockerfiles'
            }
        }
    }
}
