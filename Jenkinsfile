pipeline {
    agent any

    tools {
        maven 'maven' // Assure-toi que ce nom correspond à celui défini dans Jenkins (Global Tool Configuration)
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage("Clean up") {
            steps {
                deleteDir() // Supprime tous les fichiers du workspace Jenkins
            }
        }

        stage("Clone repo") {
            steps {
                sh "git clone https://github.com/israhadjhassine/exp1spring.git"
            }
        }

        stage("Generate backend image") {
            steps {
                dir("exp1spring") {
                    sh "mvn clean install"
                    sh "docker build -t hello-world ."
                }
            }
        }

        stage("Run docker compose") {
            steps {
                dir("exp1spring") {
                    sh "docker-compose up -d"
                }
            }
        }
    }
}
