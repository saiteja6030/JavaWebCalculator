node{
	stage('SCM Checkout')
 	{
 		sshagent(['private'])
			{
			git branch: 'kubernetives', url: 'https://github.com/saiteja6030/JavaWebCalculator.git'
			}
	}
		
	stage('Execute kubectl commands')
	{
		
		def K8start = 'kubectl apply -f app.yml'
		sshagent(['private'])
		{
			sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.38.32 ${K8start}"
		}
	}

}
