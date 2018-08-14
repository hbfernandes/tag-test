pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
              echo 'Building stuff' 
            }
        }
        stage('Tag') { 
            steps {
                 withCredentials([
                   usernamePassword(
                     credentialsId: 'github-buildguy', 
                     passwordVariable: 'GIT_PASSWORD', 
                     usernameVariable: 'GIT_USERNAME')]) {
                        sh("git tag -a ${env.BUILD_NUMBER} -m 'Jenkins'")
                        sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/hbfernandes/tag-test.git --tags')
                    }
            }
        }
    }
}