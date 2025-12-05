pipeline {
    agent any
    
    tools {
        maven 'M3'
        jdk 'JDK17'
    }
    
    triggers {
        githubPush()
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/rohi16122006/maven-project-build.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
    
    post {
        success {
            echo 'Build completed successfully!'
            echo "JAR file generated at: ${WORKSPACE}/target/maven-project-build-1.0-SNAPSHOT.jar"
        }
        failure {
            echo 'Build failed!'
        }
    }
}
