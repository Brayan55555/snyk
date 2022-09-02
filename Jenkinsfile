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
                sh 'sudo docker build -t hello-brayan .'
            }
        }
        stage('Registrando Imagen') {
            steps {
                sh "sudo docker tag hello-brayan brayanumba/hello-brayan:v1"
            }
        }
        stage('Push') {
            steps {
                sh "sudo docker push brayanumba/hello-brayan:v1"
            }
        }
        stage('Scan') {
            steps {
                sh "sudo docker scan hello-brayan"
            }
        }            
    }
}