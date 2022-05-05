pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MAVEN"
    }

    stages {
        stage('Build Maven') {
            steps {
                // Get some code from a GitHub repository
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/zahir012/Docker_build_and_push_using_Maven_Jenkins_Pipeline.git']]])

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
            }

        }
        
        stage('Build Docker image') {
            
            steps {
                
                script { 
                    
                    sh 'docker build -t zahirul012/java-app-1.0 .'
                    
                }
                
            }
            
        }    
            
        stage('Push docker image to docker hub') {
            
            steps {
                
                script {
                    
                    withCredentials([string(credentialsId: 'docker', variable: 'docker')]) {
                    sh 'docker login -u zahirul012 -p ${docker}'
                    }
                    
                    sh 'docker push zahirul012/java-app-1.0'
                    
                }
            }
        }
            
    }
    
}
