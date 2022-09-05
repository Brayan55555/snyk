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
        stage("My stage") {            
        steps {
            bat label: 'My batch script',
                script: ''' @echo off
                            return_1_if_success.exe   // command which returns 1 in case of success, 0 otherwise
                            IF %ERRORLEVEL% EQU 1 (exit /B 0) ELSE (exit /B 1)'''
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
                sh "sudo docker scan --accept-license hello-php"
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