pipeline{
    
    agent any
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/BalajNaidu-7013/demo-counter-app.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        // stage('Static code analysis'){
            
        //     steps{
                
        //         script{
                    
        //             withSonarQubeEnv(credentialsId: 'sonar-api') {
                        
        //                 sh 'mvn clean package sonar:sonar'
        //             }
        //            }
                    
        //         }
        //     }
        //     stage('Quality Gate Status'){
                
        //         steps{
                    
        //             script{
                        
        //                 waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
        //             }
        //         }
        //     }

        stage('nexus artifact uploader'){
            steps{
                script{
                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'springboot',
                             classifier: '', 
                             file: 'target/springboot-1.0.0.jar',
                              type: 'jar'
                        ]
                    ], 
                            credentialsId: 'nexus-cred', 
                            groupId: 'com.example',
                            nexusUrl: '54.175.109.72:8081',
                            nexusVersion: 'nexus3',
                            protocol: 'http', 
                            repository: 'http://54.175.109.72:8081/repository/mrdevopsapp-release/', 
                            version: '1.0.0'
                }
            }
        }
        }

}