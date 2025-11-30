pipeline {
    agent any
    stages {
        stage('Build Maven') {
            steps {
                sh 'pwd'
                sh 'mvn clean install package'
            }
        }
        stage('Copy Artifacts') {
            steps {
                sh 'pwd'
                sh 'cp -r target/*.jar docker'
            }
        }
        stage('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def customImage = docker.build("xilinx19/petclinic:${env.BUILD_NUMBER}", "./docker")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        customImage.push()
                    }
                }
            }
        }
        stage('Build on kubernetes') {
            steps {
                withKubeConfig([credentialsId: 'kubeconfig']) {
                    // Copy chart into workspace, just like before
                    sh 'pwd'
                    sh 'cp -R helm/* .'
                    sh 'ls -ltrh'
                    sh 'pwd'

                    // 1) Open SSH tunnel Jenkins -> kind host for API port 44569
                    sh '''
                    ssh -i /var/lib/jenkins/.ssh/Devops.pem \
                        -o StrictHostKeyChecking=no \
                        -f -N \
                        -L 127.0.0.1:44569:127.0.0.1:44569 \
                        ubuntu@43.205.229.214
                    '''

                    // 2) Run helm using the kubeconfig injected by withKubeConfig
                    sh "helm upgrade --install petclinic-app petclinic --set image.repository=xilinx19/petclinic --set image.tag=${BUILD_NUMBER}"
                }
            }
        }
    }
}
