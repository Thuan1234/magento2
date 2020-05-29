pipeline {
    agent {
        node {
            label 'g1test'
            customWorkspace "/var/www/html/g1/jenkinsDemo"
        }
    }
    stages {
        stage("foo") {
            steps {
                echo "Workspace dir is ${pwd()}"
            }
        }
        stage('Build Image') {
                steps {
                    script {
                        sh "echo pwd"
                        sh "${phpBin} bin/magento setup:upgrade"
                    }
                }
            }
    }
    post {
        cleanup {
            /* clean up tmp directory */
            dir("${workspace}@tmp") {
                deleteDir()
            }
            /* clean up script directory */
            dir("${workspace}@script") {
                deleteDir()
            }
        }
    }
}
