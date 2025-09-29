pipeline {

  agent any

  environment {
    dockerimagename = "ujwalnagrikar/my-app:v1"
    dockerImage = ""
    registryCredential = "dockerhublogin"
  }

  stages {

    stage('Checkout Source') {
      steps {
        git branch: 'main',
            url: 'https://github.com/UjwalNagrikar/CI-CD-Pipleline-for-Kubernetes-Deployment-.git'
      }
    }

    stage('Build image') {
      steps {
        script {
          dockerImage = docker.build(dockerimagename)
        }
      }
    }

    stage('Pushing Image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(
            configs: "deploymentservice.yml",
            kubeconfigId: "kubernetes"
          )
        }
      }
    }
  }
}
