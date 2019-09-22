pipeline {
    agent any
    environment {
        // Removed other variables for clarity...
        SFDX_USE_GENERIC_UNIX_KEYCHAIN = true
        HUB_ORG=env.HUB_ORG_DH
        SFDC_HOST = env.SFDC_HOST_DH
        JWT_KEY_CRED_ID = env.JWT_CRED_ID_DH
        CONNECTED_APP_CONSUMER_KEY=env.CONNECTED_APP_CONSUMER_KEY_DH
        // ...
    }
    stages {
        stage('TEST') {
            steps {
                withCredentials([file(credentialsId: JWT_KEY_CRED_ID, variable: 'VAR_CERT_FILE')]) {
                    bat returnStdout: true, script: "${toolbelt}/sfdx force:auth:jwt:grant --clientid ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile ${VAR_CERT_FILE} --setdefaultdevhubusername --instanceurl ${SFDC_HOST}"
                }
            }
        }
    }
}