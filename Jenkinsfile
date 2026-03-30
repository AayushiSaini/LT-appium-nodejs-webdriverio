pipeline {
    agent any

    environment {
        LT_USERNAME   = credentials('LT_USERNAME')
        LT_ACCESS_KEY = credentials('LT_ACCESS_KEY')
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
                dir('android-sample') { sh 'npm install' }
                dir('ios-sample') { sh 'npm install' }
            }
        }

        stage('Android - App & Web (Single & Parallel)') {
            steps {
                dir('android-sample') {
                    sh 'npx wdio android_ltOptions_w3c/android-app-single-ltOptions-w3c.conf.js --spec ../specs/android-test.js'
                    sh 'npx wdio android_ltOptions_w3c/android-web-single-ltOptions-w3c.conf.js --spec ../specs/android-web-test.js'
                    sh 'npx wdio android-parallel.conf.js --spec ../specs/android-test.js'
                    sh 'npx wdio android-web-parallel.conf.js --spec ../specs/android-web-test.js'
                }
            }
        }

        stage('iOS - App & Web (Single & Parallel)') {
            steps {
                dir('ios-sample') {
                    sh 'npx wdio ios_ltOptions_w3c/ios-app-single-ltOptions-w3c.conf.js --spec ../specs/ios-test.js'
                    sh 'npx wdio ios_ltOptions_w3c/ios-web-single-ltOptions-w3c.conf.js --spec ../specs/ios-web-test.js'
                    sh 'npx wdio ios-parallel.conf.js --spec ../specs/ios-test.js'
                    sh 'npx wdio ios-web-parallel.conf.js --spec ../specs/ios-web-test.js'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/errorShots/*.png', allowEmptyArchive: true
            deleteDir()
        }
    }
}