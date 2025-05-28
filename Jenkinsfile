pipeline {

    agent any

    environment {

        IMAGE_NAME = 'sagarika345/myapp'

        TAG = 'latest'

    }

    stages {

        stage('Build Docker Image') {

            steps {

                script {

                    docker.build("${IMAGE_NAME}:${TAG}")

                }

            }

        }

        stage('Push to DockerHub') {

            steps {

                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {

                    script {

                        sh """

                            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin

                            docker push ${IMAGE_NAME}:${TAG}

                        """

                    }

                }

            }

        }

    }

    post {

        always {

            sh 'docker logout'

        }

    }

}
