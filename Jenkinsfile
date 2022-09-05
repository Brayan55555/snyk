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
                sh "sudo docker tag hello-php brayanumba/hello-php:v1"
            }
        }
        stage('Push') {
            steps {
                sh "sudo docker push brayanumba/hello-php:v1"
            }
        }       
        stage('Scan') {
            try {
                sh "sudo docker scan --json hello-php"
                } catch (e) { echo "Caught exception: ${e}"
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