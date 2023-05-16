pipeline {
  agent any

  stages {
    stage('Namespace Check') {
      steps {
        script {
          try {
            def nsExists = sh(returnStdout: true, script: 'kubectl get namespace wp')
            if (nsExists) {
              echo "Namespace wp already exists"
            } else {
              echo "Creating namespace wp"
              sh 'kubectl create namespace wp'
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
            def chartName = 'final-project-wp-scalefocus'
            def releaseName = 'wp'

            def chartExists = sh(returnStdout: true, script: "helm list -q ${releaseName} --namespace wp")
            if (chartExists) {
              echo "Chart ${releaseName} already exists"
            } else {
              echo "Installing chart ${chartName} as ${releaseName}"
              sh "helm install ${releaseName} bitnami/wordpress --namespace wp -f /bitnami/wordpress/values.yaml --set service.type=ClusterIP"
            }
          } catch (Exception e) {
            echo "Error installing Helm chart: ${e.getMessage()}"
          }
        }
      }
    }
  }
}
