pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat """
                if exist out rmdir /s /q out
                mkdir out
                javac -d out src\\Calculator.java
                """
            }
        }

        stage('Run') {
            steps {
                bat """
                java -cp out Calculator
                echo Build_OK > artifact.txt
                """
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'artifact.txt, out/**', allowEmptyArchive: false
        }
    }
}