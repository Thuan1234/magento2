pipeline {
    agent {
        node {
            label 'demo_slave'
            customWorkspace "/var/www/html/g1/jenkinsDemo"
        }
    }
    stages {
        stage("foo") {
            steps {
                echo "Workspace dir is ${pwd()}"
            }
        }
        stage('Deployment') {
             steps {
                 script {
                    sh "php bin/magento setup:upgrade"
                    sh "php bin/magento setup:static-content:deploy -f"
                    sh "php bin/magento c:f"
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
