pipeline {
    agent {
        node {
            label 'g1apache'
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
                    sh "su -s /bin/bash apache <<< @htadmin2016"
                    sh 'whoami'
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
