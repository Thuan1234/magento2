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
node {
    def remote = [:]
        remote.name = 'g1test'
        remote.host = '72.arrowhitech.net'
        remote.port = 22222
        remote.user = 'aht_g1'
        remote.password = '@htG1999'
        remote.allowAnyHosts = true
    stage('Remote SSH') {
        sshCommand remote: remote, command: "su -s /bin/bash apache <<< '@htadmin2016';cd jenkinsDemo/;rm -rf /generated/code;php bin/magento setup:upgrade;php bin/magento setup:static-content:deploy -f;php bin/magento cache:clean;php bin/magento cache:flush;php bin/magento indexer:reindex"
    }
}
