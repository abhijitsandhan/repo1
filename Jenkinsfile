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
                  
                }
            }
        }
        
        stage('Maven Install') {
            steps {
                script {
                    /**
                     * Override maven in this stage
                     * you can also use 'tools {maven: "$mavenLocation"}'
                     *
                     * globalMavenSettingsConfig: Select a global maven settings element from File Config Provider
                     * jdk: Select a JDK installation
                     * maven: Select a Maven installation
                     */
                    withMaven {
                        /**
                         * To proceed to the next stage even if the current stage failed,
                         * enclose this stage in a try-catch block
                         */
                        try {
                            sh "mvn -f DemoMavenProject/pom.xml clean install"
                        } catch (Exception err) {
                            echo 'Maven clean install failed'
                            currentBuild.result = 'FAILURE'
                        } finally {
                            publishHTMLReports('Reports')
                        }
                    }
                }
            }
        }
    }
}
