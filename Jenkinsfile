    pipeline {
        agent {
            docker {
                image 'node:16-buster-slim'
                args '-p 3000:3000'
            }
        }
        stages {
            stage('Build') {
                steps {
                    sh 'npm install'
                }
            }
            stage('Manual Approval') { 
                steps {
                    input message: 'Lanjutkan ke tahap Deploy?' 
                }
            }
            stage('Deploy') { 
                options {
                    timeout(time: 1, unit: 'MINUTES')
                }
                steps {
                    sh './jenkins/scripts/deliver.sh' 
                    input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
                    sh './jenkins/scripts/kill.sh' 
                }
            }
            stage('Test') { 
                steps {
                    sh './jenkins/scripts/test.sh' 
                }
            } 
        }
    }
