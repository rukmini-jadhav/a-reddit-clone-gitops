pipeline {
    agent any 
    stages {
        stage('cleanup workspace') {
            steps{
                cleanWs()
            }
        }
        stage('checkout from scm') {
            steps{
                git branch: 'main', url: 'https://github.com/rukmini-jadhav/a-reddit-clone-gitops.git'
                }
         }
        stage('update the deployment tags') {
            steps {
                sh """
                  cat deployment.yaml
                  sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml
                """
            }
        }
        stage("push the changed deployment file to github") {
            steps {
                sh """
                 git config --global user.name "rukmini-jadhav"
                 git config --global user.email "rukminijadhav7066@gmail.com"
                 git add deployment.yaml
                 git commit -m "updated deployment manifest"
                """
                 withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                    sh "git push https://github.com/Ashfaque-9x/a-reddit-clone-gitops.git main"

            }
        }
   }
}
