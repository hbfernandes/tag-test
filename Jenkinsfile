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

script {            

                    def cred = sshUserPrivateKey(
                      credentialsId: 'github-buildguy-ssh',
                      usernameVariable: 'GIT_USERNAME', 
                      keyFileVariable: 'GITHUB_KEY')
                    def envi = [
                            'GIT_COMMITTER_NAME=$GIT_USERNAME', 
                            'GIT_COMMITTER_EMAIL=$GIT_USERNAME@hitachivantara.com', 
                            'GIT_SSH_COMMAND=ssh -i $GITHUB_KEY -o StrictHostKeyChecking=no']
                  withCredentials([cred]) {
                        // sh "git config user.name $GIT_USERNAME"
                        // sh "git config user.email $GIT_USERNAME"

                        // sh 'echo ssh -i $GITHUB_KEY -l git -o StrictHostKeyChecking=no \\"\\$@\\" > run_ssh.sh'
                        // sh 'chmod +x run_ssh.sh'
                        withEnv(envi) {    
                            
                            sh("git tag -a ssh-${env.BUILD_NUMBER} -m 'Jenkins'")
                            sh("""
                                git push git@github.com:hbfernandes/tag-test.git --tags
                            """)
                        }
                  }
}
            }
        }
    }
}