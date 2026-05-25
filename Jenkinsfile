@Library('shared-lib') _

pipeline {

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
                script{
                    def x = new edu.iti.mavenClass()
                    x.build("package install -DskipTests")
                }
                
            }
        }

        stage('Archive Java App') {
            steps {
                archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
            
            }
        }
        stage ('Test Java App')
        {
            steps{
                 script{
                    def x = new edu.iti.mavenClass()
                    x.test()                }

            }
        }
        

        stage('Build Docker Image') {
            steps {
                script {
                    def x = new edu.iti.dockerclass
                    x.build("maiwael/java" , "v1")

                }
               // sh 'docker build -t java-app:v1 .'
            }
        }

        stage('Docker Login') {
            steps {
                script{
                    def x2 = new edu.iti.dockerclass
                    x2.login("${dockerUsername}" , "${dockerPassword}" )
                }
              //  sh 'docker login -u ${dockerUsername} -p ${dockerPassword}'
            }
        }

        // stage('Push Docker Image') {
          //   steps {
            //     sh 'docker push java-app:v1'
            // }
        // }

    }
}


/*
node {

    stage('Clone Repository') {
        git branch: 'main',
        url: 'https://github.com/MaiWael25/cicd.git'
    }

    stage('Build') {
        sh 'mvn clean package'
    }

    stage('Test') {
        sh 'mvn test'
    }
}
*/
