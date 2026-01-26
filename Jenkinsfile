pipeline {
    agent any

    environment {
        LT_USERNAME   = credentials('LT_USERNAME')
        LT_ACCESS_KEY = credentials('LT_ACCESS_KEY')
    }

    stages {
        stage('Install Root Dependencies') {
            steps {
                // Root folder ki dependencies (specs access ke liye)
                sh 'npm install'
            }
        }

        stage('Android - All Tests') {
            steps {
                dir('android-sample') {
                    sh 'npm install'
                    echo 'Running Android Single, Parallel, and Web tests...'
                    // Single App Test
                    sh 'npx wdio android_ltOptions_w3c/android-app-single-ltOptions-w3c.conf.js --spec ../specs/android-test.js'
                    // Parallel App Test
                    sh 'npx wdio android-parallel.conf.js --spec ../specs/android-test.js'
                    // Web Single Test
                    sh 'npx wdio android_ltOptions_w3c/android-web-single-ltOptions-w3c.conf.js --spec ../specs/android-web-test.js'
                }
            }
        }

        stage('iOS - All Tests') {
            steps {
                dir('ios-sample') {
                    sh 'npm install'
                    echo 'Running iOS Single and Parallel tests...'
                    // Single iOS Test
                    sh 'npx wdio ios_ltOptions_w3c/ios-app-single-ltOptions-w3c.conf.js --spec ../specs/ios-test.js'
                    // Parallel iOS Test
                    sh 'npx wdio ios-parallel.conf.js --spec ../specs/ios-test.js'
                }
            }
        }
    }
}
