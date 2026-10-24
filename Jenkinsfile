pipeline{
    agent any

    stages{
         stage("1 SonarQube scanner"){
            steps{
                echo "SonarQube Scan"
              withSonarQubeEnv("SonarQube"){
                 sh '''
                 sonar-scanner \
                -Dsonar.projectKey=my-personal \
                 -Dsonar.sources=. \
                 -Dsonar.host.url=http://13.221.84.115:9000 \
                 -Dsonar.login=sqa_4202215858d710d2845cba76489b5afc76812ec7

                 '''
                 
              }
            }
         }
        stage("this is image Build Stage"){
            steps {
                echo "Build docker Image......."
                sh "docker build -t devopsaditya123/pyfile:v1 ."
            }
        }
        stage("Push the image in docker hub"){
            steps{
                withCredentials([usernamePassword(credentialsId: "docker-pass", usernameVariable: "USER", passwordVariable: "PASS")]){
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push devopsaditya123/pyfile:v1"
                }
            }
        }
    }
}