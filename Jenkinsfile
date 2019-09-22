pipeline {
    agent any
    environment {
        // Removed other variables for clarity...
        SFDX_USE_GENERIC_UNIX_KEYCHAIN = true
        HUB_ORG='admin.user@dev.org'
        SFDC_HOST = 'https://login.salesforce.com'
        JWT_KEY_CRED_ID = credentials('9fa85236-84d8-4fa5-bf6d-3b83868a31e5')
        CONNECTED_APP_CONSUMER_KEY='3MVG96_7YM2sI9wTTpIpn2FVO.Mm.HxpHNFZDs_.bPGJDE.EranWdiaIe9D2mXaM7p00ZhQ0y7hO2v9YEy_QS'
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