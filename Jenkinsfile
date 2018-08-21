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
                //  withCredentials([
                //    usernamePassword(
                //      credentialsId: 'github-buildguy', 
                //      passwordVariable: 'GIT_PASSWORD', 
                //      usernameVariable: 'GIT_USERNAME')]) {
                //         sh "git config user.name $GIT_USERNAME"
                //         sh "git config user.email $GIT_USERNAME"

                //         sh("git tag -a http-${env.BUILD_NUMBER} -m 'Jenkins'")
                //         sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/hbfernandes/tag-test.git --tags')
                //     }


                  withCredentials([
                    sshUserPrivateKey(
                      credentialsId: 'github-buildguy-ssh',
                      usernameVariable: 'GIT_USERNAME', 
                      keyFileVariable: 'GITHUB_KEY')]) {
                        sh "git config user.name $GIT_USERNAME"
                        sh "git config user.email $GIT_USERNAME"
                        
                        // sh 'echo ssh -i $GITHUB_KEY -l git -o StrictHostKeyChecking=no \\"\\$@\\" > run_ssh.sh'
                        // sh 'chmod +x run_ssh.sh'
                        withEnv(['GIT_SSH_COMMAND="/usr/bin/ssh -i '+GITHUB_KEY+' -o StrictHostKeyChecking=no"']) {    
                            sh 'echo $GIT_SSH_COMMAND > run_ssh.sh'
                            sh("git tag -a ssh-${env.BUILD_NUMBER} -m 'Jenkins'")
                            sh('git push git@github.com:hbfernandes/tag-test.git --tags')
                        }
                  }
            }
        }
    }
}