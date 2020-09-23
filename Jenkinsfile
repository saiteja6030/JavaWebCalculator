node{
   stage('SCM Checkout'){
       git branch: 'master', url: 'https://github.com/saiteja6030/JavaWebCalculator.git'
   }
   stage('Mvn Package'){
     def mvnHome = tool name: 'maven-3', type: 'maven'
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} clean package"
   }
   stage('Build Docker Image'){
     sh 'docker build -t 8639628479/tomcatdocker:tomcatdevops .'
   }
   stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u 8639628479 -p ${dockerHubPwd}"
     }
     sh 'docker push 8639628479/tomcatdocker:tomcatdevops'
   }
   stage('Run Container on Dev Server'){
     def dockerRun = 'docker run -d --name tomcatcontainer -p 8080:8080 8639628479/tomcatdocker:tomcatdevops'
     sshagent(['dev-server']) {
       sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.18.198 ${dockerRun}"
     }
   }
}



}