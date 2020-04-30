#!/usr/bin/env groovy

pipeline {
  agent { label 'docs' }
  stages {
    stage('Build') {
      steps {
        sh "env"
        script { 
          env.GIT_COMMIT_MSG = sh (
            script: "git log --format=%B -n 1 ${env.GIT_COMMIT} | head -n 1",
            returnStdout: true).trim() 
          env.GIT_AUTHOR_NAME = sh ( 
            script: "git show -s --pretty=%an ${env.GIT_COMMIT}",
            returnStdout: true).trim() 
          env.BUILD_INFO = "<${env.RUN_DISPLAY_URL}|${env.JOB_NAME} [${env.BUILD_NUMBER}]> submitted by ${env.GIT_AUTHOR_NAME} with commit <https://github.com/juji-io/docs/commit/${env.GIT_COMMIT}|${env.GIT_COMMIT.take(7)}>: ${env.GIT_COMMIT_MSG}"
        }
        sh '''
          git pull
          mkdocs build
          cd ../juji-io.github.io 
          mkdocs gh-deploy --config-file ../juji-io_on_github_docs_master/mkdocs.yml --remote-branch master
        '''
      }
    }
  }
  post {
    success {
      slackSend (color: '#00FF00', message: "SUCCESSFUL: Job ${env.BUILD_INFO}")
    }
    aborted {
      slackSend (color: '#FF00FF', message: "ABORTED: Job ${env.BUILD_INFO}")
    }
    notBuilt {
      slackSend (color: '#AAAAAA', message: "NOT_BUILT: Job ${env.BUILD_INFO}")
    }
    unstable {
      slackSend (color: '#FFFF00', message: "UNSTABLE: Job ${env.BUILD_INFO}")
    }
  }
}

