pipeline {
  environment {
      registry = "kmcourter/addrbook"
      registryCredential = 'Colleen92'
    }
agent any
stages {
    stage ('Build Image'){
    steps {
        script {
        dockerImage = docker.build.registry + ":$BUILD_NUMBER"
        }

    }
    }
    stage ('Deploy){
    steps {
        script {
        docker.withRegistry( '', 'Colleen92') {
            dockerImage.push()
        }
        }

    }
    } 
    stage ('Delete) {
    steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
    }
    }
  }
}
node {
    stage ('Execute Image'){
        def appImage = docker.build("kmcourter/addrbook:${enf.BUILD_NUMBER}")
        customImage.inside {
            sh 'echo Pretend this is an application.'
        }
    }
}