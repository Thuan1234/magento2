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
        stage('Remote SSH') {
        def remote = [:]
                    remote.name = 'g1test'
                    remote.host = '72.arrowhitech.net'
                    remote.port = '22222'
                    remote.user = 'apache'
                    remote.password = '@htadmin2016'
                    remote.allowAnyHosts = true
          sshCommand remote: remote, command: "rm -rf /generated/code"
          sshCommand remote: remote, command: "php bin/magento setup:upgrade"
          sshCommand remote: remote, command: "php bin/magento setup:static-content:deploy -f"
          sshCommand remote: remote, command: "php bin/magento cache:clean"
          sshCommand remote: remote, command: "php bin/magento cache:flush"
          sshCommand remote: remote, command: "php bin/magento indexer:reindex"
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
