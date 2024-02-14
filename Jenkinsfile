pipeline{
   agent any
   stages {
        stage("prepare"){
                   steps {
                            sh "true"
                   }
        }
        stage("Deploy"){
         withCredentials([usernameColonPassword(credentialsId: 'k3s-admin-user', variable: 'KUBECONFIG')]) {
                 sh "kubectl get no"
          }
        }
   }

}
