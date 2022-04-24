pipeline {
	agent any
	stages {
		stage('git scm update') {
			steps {
				git url: 'https://github.com/tenny2188/testjenkins.git', branch: 'master'
			}
		}
		stage('docker build and push') {
			steps {
				sh '''
				sudo docker build -t tenny210/myweb:1.0 .
				sudo docker push tenny210/myweb:1.0
				'''
			}
		}
		stage('deploy k8s') {
			steps {
				sh '''
				kubectl create deploy testpipeline --image=brian24/myweb:1.0
				kubectl expose deploy testpipeline --type=NodePort --port=8081 \
				--target-port=80 --name=testpipeline-svc
				'''
			}
		}
	}
}
