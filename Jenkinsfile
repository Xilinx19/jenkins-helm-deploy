pipeline {
    agent any 
        stages {
            stage ('build maven') {
                steps {
                    sh 'pwd'
                    sh 'mvn clean install package'

                }
            
            }
            stage ('copy artifacts') {
                steps{
                    sh 'pwd'
                    sh 'cp -r  target/*.jar docker'
                }
            }
            stage ("test") {
                steps {
                    sh 'mvn test'
                }
            }
        }
    }