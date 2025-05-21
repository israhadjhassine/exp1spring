pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Nettoyage') {
            steps {
                deleteDir()
            }
        }
        stage('Clonage du dépôt') {
            steps {
                sh 'git clone https://github.com/israhadjhassine/exp1spring.git'
            }
        }
        stage('Génération de l\'image backend') {
            steps {
                dir('exp1spring') {
                    sh 'mvn clean install'
                    sh 'docker build -t hello-world .'
                }
            }
        }
        stage('Exécution de Docker Compose') {
            steps {
                dir('exp1spring') {
                    sh 'docker compose up -d'
                }
            }
        }
    }
}
