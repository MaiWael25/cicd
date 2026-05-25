/*pipeline {

    agent {
        label 'jenkins-agent'
    }

    tools {
        jdk 'jdk-11'
        maven 'maven-354'
    }

    environment {
        dockerUsername = credentials('docker-username')
        dockerPassword = credentials('docker-password')
    }

    stages {

        stage('Build Java App') {
            steps {
                sh 'mvn package install -DskipTests'
            }
        }

        stage('Archive Java App') {
           */ // steps {
            //    archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
            /*
            }
        }
        

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t java-app:v1 .'
            }
        }

        stage('Docker Login') {
            steps {
                sh 'docker login -u ${dockerUsername} -p ${dockerPassword}'
            }
        }

        // stage('Push Docker Image') {
          //   steps {
            //     sh 'docker push java-app:v1'
            // }
        // }

    }
}
*/

node {

 /*   stage('Clone') {
        git 'https://github.com/yourusername/java-project.git'
    }
    */

 node('jenkins-agent') {

    stage('Build') {
        sh 'javac App.java'
    }

    stage('Run') {
        sh 'java App'
    }

    stage('List Files') {
        sh 'ls -l'
    }

    stage('Current User') {
        sh 'whoami'
    }

    stage('Java Version') {
        sh 'java -version'
    }

    cleanWs()
}
}