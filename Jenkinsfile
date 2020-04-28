node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "hello-kenzan"
    registryHost = "bendevet/"
    imageName = "bendevet/milan:latest"
    env.BUILDIMG=imageName

    stage "Build"
    
        sh "docker build -t ${imageName} -f applications/hello-kenzan/Dockerfile applications/hello-kenzan"
    
    //stage "Push"

       // sh "docker push ${imageName}"
    docker.withRegistry('https://www.docker.com/', 'bendevetdocker') {
         sh "docker push ${imageName}"
        //def customImage = docker.build('bendevet/milan:latest')

        /* Push the container to the custom Registry */
       // customImage.push()
    }

    stage "Deploy"

        kubernetesDeploy configs: "applications/${appName}/k8s/*.yaml", kubeconfigId: 'kenzan_kubeconfig'

}
