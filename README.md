# codincity
Assessment
MyPipeline


node {


 stage('Clone Repo') {

     sh 'rm -rf dockertest1'

       sh 'git clone https://github.com/basha202/dockertest1.git'

 }


 stage('Build Docker Image') {

     sh 'cd /var/lib/jenkins/workspace/pipeline1/dockertest1'

     sh ' cp  /var/lib/jenkins/workspace/pipeline1/dockertest1/* /var/lib/jenkins/workspace/pipeline1'

  sh 'docker build -t Scmmohammad/pipelinetest:v1 .'

 }


 stage('Push Image to Docker Hub') {

  sh 'docker push Scmmohammad/pipelinetest:v1'

 }


 stage('Deploy to Docker Host') {

  sh 'docker -H tcp://10.1.1.250:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 --network ansible_nw Scmmohammad/pipelinetest:v1'

 }


 stage('Check WebApp Rechability') {

   sh 'curl http://ec2-3-80-165-76.compute-1.amazonaws.com:9000'

 }


}
