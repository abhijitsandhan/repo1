pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                cleanWs()
                echo 'workspace cleanup completed'
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'a', url: 'https://github.com/abhijitsandhan/repo1.git']]])
            }
        }
        stage ('zip') {
            steps {
                script{
                  //zip archive: false, dir: 'folder1', glob: '', zipFile: 'files.zip'
                  //zip zipFile: 'test.zip', archive: false, dir: 'folder1'
                  sh 'zip -r test.zip .'
                  sh 'ls'
                    sh 'mvn -v'
                }
            }
        }
    }
}
