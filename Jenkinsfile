pipeline {
    agent any

    stages {
      stage('Clonage du dépôt GitHub') {
            steps {
                git branch: 'main', url: 'https://github.com/csurqunix/OSDetector.git'
                
            }
        }
        stage('Installation de Python et de Pip'){
            steps {
                sh 'sudo apt-get install -y python3.11'
                sh 'curl -sS https://bootstrap.pypa.io/get-pip.py | sudo python3.11'
            }
              }
        stage('Execution du code'){
            steps {
                sh 'python os_detector.py'
            }
        }
        stage('Setting permissions and running the script') {
            steps {
                sh 'chmod +x OSDetector.py'
                sh 'python3 OSDetector.py'
            }
        }
    }

    post {
        success {
            echo 'It worked, you Geniuuuus !'
        }
        failure {
            echo 'Ohh god, we are in troubles'
            script {
                def emailBody = "Bonjour,\n\nLa construction et l'exécution du script ont échoué. Veuillez vérifier les journaux de construction Jenkins pour plus de détails.\n\nCordialement,\nL'équipe DevOps"
                emailext (
                    subject: 'Échec de la construction Jenkins',
                    body: emailBody,
                    recipientProviders: [[$class: 'CulpritsRecipientProvider']],
                    to: 'cedsurq@protonmail.com'
                )
            }
        }
    }
}
