pipeline {
	agent any
    stages { 	
        stage('pull latest code') {
            steps {
                git 'https://github.com/DaSweer/Dockerd.git'
            }
        }
        stage('spining up docker images'){
        	steps {
        			sh 'docker-compose up -d'
        		}
        }
        
        stage('Build') {
            steps {
            	sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('test') {
            steps {
                 sh 'mvn test'
                }
        } 
        stage('Destroy - After running tests on Containers') {
        	steps {
        		sh 'docker stop $(docker ps -a -q)'
        		sh 'docker rm $(docker ps -a -q)'
        		}
        }
              
    }
}