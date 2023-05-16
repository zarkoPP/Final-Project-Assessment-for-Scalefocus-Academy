pipeline {
  agent any

  stages {
    stage('Namespace Check') {
      steps {
        script {
          try {
            def os = isUnix() ? 'unix' : 'windows'
            def nsExists = os == 'unix' ? sh(returnStdout: true, script: 'kubectl get namespace wp') : bat(returnStdout: true, script: 'kubectl get namespace wp')
            if (nsExists) {
              echo "Namespace wp already exists"
            } else {
              echo "Creating namespace wp"
              if (os == 'unix') {
                sh 'kubectl create namespace wp'
              } else {
                bat 'kubectl create namespace wp'
              }
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
            def os = isUnix() ? 'unix' : 'windows'
            def chartName = 'final-project-wp-scalefocus'
            def releaseName = 'wp'

            def chartExists = os == 'unix' ? sh(returnStdout: true, script: "helm list -q ${releaseName} --namespace wp") : bat(returnStdout: true, script: "helm list -q ${releaseName} --namespace wp")
            if (chartExists) {
              echo "Chart ${releaseName} already exists"
            } else {
              echo "Installing chart ${chartName} as ${releaseName}"
              if (os == 'unix') {
                sh "helm install ${releaseName} bitnami/wordpress --namespace wp -f /bitnami/wordpress/values.yaml --set service.type=ClusterIP"
              } else {
                bat "helm install ${releaseName} bitnami/wordpress --namespace wp -f bitnami/wordpress/values.yaml --set service.type=ClusterIP"
              }
            }
          } catch (Exception e) {
            echo "Error installing Helm chart: ${e.getMessage()}"
          }
        }
      }
    }
  }
}
