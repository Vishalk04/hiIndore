node{

  //Define all variables
  def app;
  def project = 'my-project'
  def appName = 'my-first-microservice'
  def serviceName = "${appName}-backend"  
  def imageVersion = 'development'
  def namespace = 'development'
  def imageTag = "hub.docker.com/kartikjalgaonkar/${project}/${appName}:${imageVersion}.${env.BUILD_NUMBER}"
  def feSvcName = "hi-indore"
  //Checkout Code from Git
  checkout scm
  
  //Stage 1 : Build the docker image.
 // stage('Build image') {
 //   sh 'mvn clean install'
   //   sh("docker build -t ${imageTag} .")
 //   app=docker.build("kartikjalgaonkar/hi-indore")
//  }
  
  //Stage 2 : Push the image to docker registry
//  stage('Push image to registry') {
//      docker.withRegistry('https://registry.hub.docker.com', 'docker_credentials') {
 //           app.push("${env.BUILD_NUMBER}")
 //           app.push("latest")
//}
 // }
  
  //Stage 3 : Deploy Application
  stage('Deploy Application') {
       switch (namespace) {
              //Roll out to Dev Environment
              case "development":
      //--   sh "kubectl run my-app --image=kartikjalgaonkar/hi-indore --port=8081 --kubeconfig=/home/yash/.kube/config"
   //--      sh "kubectl expose deployment my-app --type=LoadBalancer --port=8081 --target-port=8081 --kubeconfig=/home/yash/.kube/config"
       //  sh "kubectl apply -f deployment.yml --kubeconfig=/home/yash/.kube/config"
      //   sh "kubectl apply -f service.yml --kubeconfig=/home/yash/.kube/config"
       // sh "kubectl config set-cluster minikube --server=https://127.0.0.1:8443 --insecure-skip-tls-verify=true"
     //   sh "kubectl config set-context minikube --cluster=minikube --user=minikube"
     // sh "kubectl config use-context minikube"

      //   sh "minikube start --vm-driver=virtualbox"
        // sh "kubectl run my-app --image=kartikjalgaonkar/hi-indore --port=8081"
                   // Create namespace if it doesn't exist
                  
                 // sh ("minikube start")
                  sh("kubectl get ns ${namespace} --kubeconfig=/home/yash/.kube/config || kubectl create namespace ${namespace} --kubeconfig=/home/yash/.kube/config")
           //Update the imagetag to the latest version
        //           sh("sed -i.bak 's#hub.docker.com/${project}/${appName}:${imageVersion}#${imageTag}#' ./k8s/development/*.yaml")
                   //Create or update resources
           sh("kubectl --namespace=${namespace} apply -f deployment.yml --kubeconfig=/home/yash/.kube/config")
                  sh("kubectl --namespace=${namespace} apply -f service.yml --kubeconfig=/home/yash/.kube/config")
          sh ("kubectl --namespace=${namespace} apply -f ingress.yml --kubeconfig=/home/yash/.kube/config")
           //Grab the external Ip address of the service
       //  sh("echo http://`kubectl --namespace=${namespace} get service/${feSvcName} --output=json --kubeconfig=/home/yash/.kube/config | jq -r '.status.loadBalancer.ingress[0].ip'` > ${feSvcName} ")
       //  sh "kubectl get svc --kubeconfig=/home/yash/.kube/config"
        // sh "minikube service hi-indore"
      sh("echo http://`kubectl --namespace=${namespace} get service/${feSvcName} --output=json --kubeconfig=/home/yash/.kube/config | jq -r '.status.loadBalancer.ingress[0].ip'` > ${feSvcName} ")
         //sh "kubectl get svc hi-indore -n hi-indore \
    //-o jsonpath= '{.status.loadBalancer.ingress[*].ip}' --kubeconfig=/home/yash/.kube/config"
                   break
           

              
  }

}
}
