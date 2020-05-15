def mapBranch = ["master": "production",
                  "qa": "qa"]

pipeline {
    
  agent {
    docker {
      image 'ruby:alpine'
    }
  }

  parameters {
    choice(name: 'DEPLOY_TO',
           choices: ['master', 'qa', 'aws'],
           description: 'Choose deployment environment')
  }

  environment {
                ENVIRONMENT_NAME = "${mapBranch[params.DEPLOY_TO]}"
  }
  stages {
	  //stage('Set Default version & get dependencies') {
    //  steps {
    //    sh 'sudo yum install ruby.x86_64
    //    sh 'ruby -v'
    //    sh 'gem install sinatra -v1.4.8'
    // }
  // }

   stage('Deliver package & execute playbook') {
		 steps {
       echo "Deploying to ${mapBranch[params.DEPLOY_TO]}"
			 ansiblePlaybook credentialsId: 'vagrant-toolbox-key',
                       disableHostKeyChecking: true,
                       inventory: "inventories/${mapBranch[params.DEPLOY_TO]}/hosts.ini",
                       playbook: 'playbook.yml'
		  }
	  }
  }
}







