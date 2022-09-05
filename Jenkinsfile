pipeline {
    agent {
        label "EC2_UBUNTU"
    }
    stages {
        stage('Inicio') {
            steps {
                echo "Iniciando Escaneo"
            }
        }
        stage('Build') {
            steps {
                sh 'sudo docker build -t hello-php .'
            }
        }
        stage('Registrando Imagen') {
            steps {
                script {
                    try {
                        sh "sudo docker scan --json hello-php"
                    } catch (Exception e) {
                        echo 'Exception occurred: ' + e.toString()
                        sh 'Handle the exception!'
                    }
                }
            }
        }
        stage('Push') {
            steps {
                sh "sudo docker push brayanumba/hello-php:v1"
            }
        }       
        stage('Scan') {
            steps {
                sh "sudo docker scan --json hello-php"
            }
        }                  
    }
    post{
        always{
            emailext to: "brayanumbachisaba@gmail.com",
            subject: "Test Email",
            body: "Test",
            attachLog: true
        }
    }
}


script {
  try {
      sh "sudo docker scan --json hello-php"
  } catch (Exception e) {
      echo 'Exception occurred: ' + e.toString()
      sh 'Handle the exception!'
  }
}