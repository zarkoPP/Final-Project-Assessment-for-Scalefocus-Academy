pipeline {
  agent any

  stages {
    stage('Namespace Check') {
      steps {
        script {
          try {
            def nsExists = bat(returnStdout: true, script: 'kubectl get namespace wp')
            if (nsExists.contains('NotFound')) {
              echo "Creating namespace wp"
              bat 'kubectl create namespace wp'
            } else {
              echo "Namespace wp already exists"
            }
          } catch (Exception e) {
            echo "Error checking/creating namespace wp: ${e.getMessage()}"
          }
        }
      }
    }

    stage('Helm Install') {
      steps {
        script {
          try {
            def chartExists = bat(returnStdout: true, script: 'helm list -q wp --namespace wp')
            if (chartExists) {
              echo "Chart wp already exists"
            } else {
              echo "Installing chart wp"
              bat 'helm install wp bitnami/wordpress --namespace wp -f values.yaml --set service.type=ClusterIP'
            }
          } catch (Exception e) {
            echo "Error installing Helm chart: ${e.getMessage()}"
          }
        }
      }
    }
  }
}
