pipeline {
 agent any
 
     parameters {
              string(name: 'BUILD_ID', defaultValue: '0.4', description: 'Build Id')
    }

  stages {

    stage('Build result') {
      steps {
        sh 'docker build -t dockersamples/result ./result'
      }
    } 
    stage('Build vote') {
      steps {
        sh "docker build -t neryap/vote:${params.BUILD_ID} ./vote"
      }
    }
    stage('Build worker') {
      steps {
        sh "docker build -t neryap/worker:${params.BUILD_ID} ./worker"
      }
    }
    stage('Push result image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerbuildbot-index.docker.io', url:'') {
          sh 'docker push dockersamples/result'
        }
      }
    }
    stage('Push vote image') {
     /* when {
        branch 'master'
      }*/
      steps {
        withDockerRegistry(credentialsId: 'dockerbuildbot-index.docker.io', url:'') {
          sh "docker push neryap/vote:${params.BUILD_ID}"
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'dockerbuildbot-index.docker.io', url:'') {
          sh "docker push neryap/worker:${params.BUILD_ID}"
        }
      }
    }
  }
}