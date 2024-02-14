pipeline{
   agent any
   parameters {
        string(name: "ENV", defaultValue: "test", trim: true, description: "Environment name")
        string(name: "IMAGE_NAME", trim: true, description: "Image repository")
        string(name: "IMAGE_TAG", trim: true, description: "Image tag")
   }
   stages {
        stage("prepare"){
                   steps {
                            sh "true"
                   }
        }
        stage("Deploy"){
          steps {
                      withCredentials([file(credentialsId: 'k3s-admin-user', variable: 'KUBECONFIG')]) {
                            script {
                                 if ("$params.ENV" == "development") {
                                       sh "sed -i \"s#IMAGE_NAME#${IMAGE_NAME}#g\" dev/kustomization.yaml"
                                       sh "sed -i \"s#IMAGE_TAG#${IMAGE_TAG}#g\" dev/kustomization.yaml"
                                       sh "kubectl apply -k dev"
                                  }
                           }       
                       }    
                          
        }
     }
   }
   post {
      always {
            deleteDir()
      }
   }
}
