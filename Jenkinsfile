pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                echo 'Menunggu 1 menit agar aplikasi tetap berjalan...'
                sleep(time: 60, unit: 'SECONDS')  // Menunggu selama 1 menit
            }
        }
    }
}