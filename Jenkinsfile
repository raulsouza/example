pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'registry:5000' // Private Docker registry URL
        //DOCKER_LOCAL_IMG = 'modem-restart-svc' // Local image name used during the build
        PROM_LOCAL_IMG = 'prom/prometheus' // Local image name used during the build
        GRAF_LOCAL_IMG = 'grafana/grafana' // Local image name used during the build
        IMAGE_TAG = 'stable' // Use 'stable' tag or BUILD_NUMBER if needed
        //DOCKER_IMAGE = "${DOCKER_REGISTRY}/${DOCKER_LOCAL_IMG}:${IMAGE_TAG}" // Full image path for the private registry
        PROM_IMAGE = "${DOCKER_REGISTRY}/${PROM_LOCAL_IMG}:${IMAGE_TAG}" // Full image path for the private registry
        GRAF_IMAGE = "${DOCKER_REGISTRY}/${GRAF_LOCAL_IMG}:${IMAGE_TAG}" // Full image path for the private registry
    }

    stages {
        stage('validate files for building') {
            steps {
                script {
                    sh 'ls -lart'
                    sh 'sudo docker ps'
                }
            }
        }
        
        //stage('Build Docker Image') {
        //    steps {
        //        script {
        //            // Build the Docker image with a tag
        //            docker.build("${PROM_LOCAL_IMG}:build", "-f Dockerfile.prom .")
        //            docker.build("${GRAF_LOCAL_IMG}:build", "-f Dockerfile.graf .")
        //        }
        //    }
        //}
//        
//        stage('Tag Docker Image for Private Registry') {
//            steps {
//                script {
//                    sh "docker image tag ${PROM_LOCAL_IMG}:build ${PROM_IMAGE}"
//                    //validate the usage og immage_tag variable in this line
//                    echo "Image tagged for private registry as ${PROM_IMAGE}:${IMAGE_TAG}"
//
//                    sh "docker image tag ${GRAF_LOCAL_IMG}:build ${GRAF_IMAGE}"
//                    //validate the usage og immage_tag variable in this line
//                    echo "Image tagged for private registry as ${GRAF_IMAGE}:${IMAGE_TAG}"
//                }
//            }
//        }
//        
//        stage('Push Docker Image') {
//            steps {
//                script {
//                    // Push the tagged image to the private registry
//                    docker.withRegistry("http://${DOCKER_REGISTRY}") {
//                        docker.image("${PROM_IMAGE}").push()
//                        docker.image("${GRAF_IMAGE}").push()
//                    }
//                }
//            }
//        }
//
//
//        // LOAD KUBECONFIG FILE FROM CREDENTIALS WE CREATED EARLIER
//        stage('setup kubeconfig') {
//            steps {
//                withCredentials([file(credentialsId: 'kubeconfig-monitoring', variable: 'kubeconfig')]) {
//                    sh "cp ${kubeconfig} ${WORKSPACE}/kubeconfig"
//                    sh "echo ${BUILD_NUMBER} > ${WORKSPACE}/BUILD_NUMBER.log"
//                }
//            }
//        }
// 
//        stage('Deploy grafana to Kubernetes') {
//            steps {
//                script {
//                    //Execute commands using KUBECONFIG
//                    sh '''
//                    export KUBECONFIG=kubeconfig
//                    
//                    kubectl get po
//                    kubectl apply -f 06-grafana-deployment.yaml
//   
//                    # Capture value from BUILD_NUMBER.log
//                    CI_BN=$(cat BUILD_NUMBER.log)
//   
//                    # Output the captured value
//                    echo "this is the value of CI_BN: $CI_BN"
//   
//                    echo "kubectl patch deployment grafana -p \'{\\"spec\\":{\\"template\\":{\\"metadata\\":{\\"annotations\\":{\\"ci-build-number\\":\\""$CI_BN"\\"}}}}}\'" > patch.sh
//   
//                    cat patch.sh
//   
//                    chmod +x patch.sh
//   
//                    ./patch.sh
//   
//                    kubectl get deployment grafana -o yaml
//   
//                    '''                
//                }
//            }
//        }
//
//        stage('Deploy prometheus to Kubernetes') {
//            steps {
//                script {
//                    //Execute commands using KUBECONFIG
//                    sh '''
//                    export KUBECONFIG=kubeconfig
//                    
//                    kubectl get po
//                    kubectl apply -f 05-prometheus-deployment.yaml
//   
//                    # Capture value from BUILD_NUMBER.log
//                    CI_BN=$(cat BUILD_NUMBER.log)
//   
//                    # Output the captured value
//                    echo "this is the value of CI_BN: $CI_BN"
//   
//                    echo "kubectl patch deployment prometheus -p \'{\\"spec\\":{\\"template\\":{\\"metadata\\":{\\"annotations\\":{\\"ci-build-number\\":\\""$CI_BN"\\"}}}}}\'" > patch.sh
//   
//                    cat patch.sh
//   
//                    chmod +x patch.sh
//   
//                    ./patch.sh
//   
//                    kubectl get deployment prometheus -o yaml
//   
//                    '''                
//                }
//            }
//        }
    }

    post {
        always {
            // Clean up the workspace
            cleanWs()
            //script {
            //    // Optionally remove the local Docker image (if necessary)
            //    docker.image("${DOCKER_LOCAL_IMG}").remove()
            //}
        }
    }
}
