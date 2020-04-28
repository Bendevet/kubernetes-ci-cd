pipeline {
  environment {
    registry = "bendevet/milan"
    registryCredential = 'bendevetdocker'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/Bendevet/kubernetes-ci-cd.git'
      }
    }
    stage('Building image') {
      steps{
        script {
        //   dockerImage = docker.build registry + ":latest"
          def dockerfile = 'applications/hello-kenzan/Dockerfile'
          def customImage = docker.build(registry + ":latest", "-f ${dockerfile} ./applications/hello-kenzan")
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry("https://www.docker.com/", registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    // stage('Remove Unused docker image') {
    //   steps{
    //     sh "docker rmi $registry:$BUILD_NUMBER"
    //   }
    // }
  }
}









// node {

//     checkout scm

//     env.DOCKER_API_VERSION="1.23"
    
//     sh "git rev-parse --short HEAD > commit-id"

//     tag = readFile('commit-id').replace("\n", "").replace("\r", "")
//     appName = "hello-kenzan"
//     registryHost = "bendevet/"
//     imageName = "bendevet/milan:latest"
//     env.BUILDIMG=imageName

//     // stage "Build"
    
//     //     sh "docker build -t ${imageName} -f applications/hello-kenzan/Dockerfile applications/hello-kenzan"
    
//     //stage "Push"

//        // sh "docker push ${imageName}"
//     docker.withRegistry('https://www.docker.com/', 'bendevetdocker') {
//          sh "docker push ${imageName}"
//         //def customImage = docker.build('bendevet/milan:latest')

//         /* Push the container to the custom Registry */
//        // customImage.push()
//     }

//     stage "Deploy"

//         kubernetesDeploy configs: "applications/${appName}/k8s/*.yaml", kubeconfigId: 'kenzan_kubeconfig'

// }
