pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
                steps {
                    echo 'Application in Testing Phase…'
                    sh 'mvn test'
                }
        }
        stage('Deploy CloudHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: '67eb39c4-65d3-4084-b4ba-df314c3e07d8', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'mvn package deploy -Dpackaging=jar -DmuleDeploy -Dusername=${USERNAME} -Dpassword=${PASSWORD} -DworkerType=Micro -Dworkers=1 -Dregion=us-west-2'
                }
            }
        }
    }
}