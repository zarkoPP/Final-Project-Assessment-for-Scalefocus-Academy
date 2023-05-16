pipeline {
  agent any

  stages {
    stage('Namespace Check') {
      steps {
        script {
          try {
            def nsExists = bat(
              returnStatus: true,
              script: 'kubectl get namespace wp'
            )
            if (nsExists == 0) {
              echo "Namespace wp already exists"
            } else {
              echo "Creating namespace wp"
              bat 'kubectl create namespace wp'
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
            bat 'helm dependency build bitnami/wordpress'
            def chartExists = bat(
              returnStatus: true,
              script: 'helm list -q wp --namespace wp'
            )
            if (chartExists == 0) {
              echo "Chart wp already exists"
            } else {
              echo "Installing chart wp"
              bat 'helm install wp bitnami/wordpress --namespace wp -f bitnami/wordpress/values.yaml --set service.type=ClusterIP'
            }
          } catch (Exception e) {
            echo "Error installing Helm chart: ${e.getMessage()}"
          }
        }
      }
    }

    stage('Waiting for port ready and port forwarding') {
      steps {
        script {
          try {
            echo "Waiting for 30 seconds..."
            sleep time: 30, unit: 'SECONDS'
            echo "Wait complete."

            def podReady = sh(
              returnStdout: true,
              script: 'kubectl get pod -l app.kubernetes.io/name=wordpress -n wp -o jsonpath="{.items[0].status.conditions[?(@.type==\'Ready\')].status}"'
            ).trim()

            if (podReady == 'True') {
              echo "WordPress pod is ready"
              echo "Forwarding port to the WordPress service..."
              bat "kubectl port-forward --namespace wp svc/final-project-wp-scalefocus-wordpress 8089:80"
            } else {
              error "WordPress pod is not ready"
            }
          } catch (Exception e) {
            error "Error checking WordPress pod status: ${e.getMessage()}"
          }
        }
      }
    }
  }
}
