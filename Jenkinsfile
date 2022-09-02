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
            steps {
                sh "sudo docker scan hello-php"
                sh ""
            }
        }            
    }
    set +e
}