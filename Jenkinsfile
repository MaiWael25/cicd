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

node('jenkins-agent') {

    // Define tools
    def jdkHome = tool name: 'jdk-11', type: 'hudson.model.JDK'
    def mvnHome = tool name: 'maven-354', type: 'hudson.tasks.Maven$MavenInstallation'

    // Set environment variables
    env.JAVA_HOME = jdkHome
    env.PATH = "${jdkHome}/bin:${mvnHome}/bin:${env.PATH}"

    withCredentials([
        string(credentialsId: 'docker-username', variable: 'DOCKER_USERNAME'),
        string(credentialsId: 'docker-password', variable: 'DOCKER_PASSWORD')
    ]) {

        stage('Build Java App') {
            sh 'mvn package install -DskipTests'
        }

        
        stage('Archive Java App') {
            archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
        }
        

        stage('Build Docker Image') {
            sh 'docker build -t java-app:v1 .'
        }

        stage('Docker Login') {
            sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
        }

        /*
        stage('Push Docker Image') {
            sh 'docker push java-app:v1'
        }
        */

    }
}