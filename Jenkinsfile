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
                sh "sudo docker push brayanumba/hello-php:v1"
                } catch (e) {
                    echo "Caught exception: ${}"
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
