pipeline {
    agent {
        docker {
            image 'maven:3.9.6-eclipse-temurin-17-alpine'
        }
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Surxya/internal-portal-testing-java-selenium.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive Reports') {
            steps {
                junit 'target/surefire-reports/*.xml'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
pipeline {
    agent any

    tools {
        maven 'Maven 3' // Define this name in Jenkins → Global Tool Configuration
        jdk 'JDK 17'    // Define this name in Jenkins → Global Tool Configuration
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Surxya/internal-portal-testing-java-selenium.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive Reports') {
            steps {
                junit 'target/surefire-reports/*.xml'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
pipeline {
    agent {
        docker {
            image 'maven:3.9.6-eclipse-temurin-17'  // Or any Maven+JDK base image
            args '-v /root/.m2:/root/.m2'  // Optional: persist Maven repo cache
        }
    }
    tools {
        maven 'maven-3.9.6'
        jdk 'jdk-17'
    }
    stages {
        stage('Build & Test') {
            steps {
                sh 'mvn clean test'
            }
        }
    }
    post {
        always {
            junit 'target/surefire-reports/*.xml'
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
