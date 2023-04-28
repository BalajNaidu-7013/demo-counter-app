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
        // stage('UNIT testing'){
            
        //     steps{
                
        //         script{
                    
        //             sh 'mvn test'
        //         }
        //     }
        // }
        // stage('Integration testing'){
            
        //     steps{
                
        //         script{
                    
        //             sh 'mvn verify -DskipUnitTests'
        //         }
        //     }
        // }
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

        // stage('nexus artifact uploader'){
        //     steps{
        //         script{
        //             def readPomVersion = readMavenPom file: 'pom.xml'

        //             def nexusRepo = readPomVersion.version.endsWith("SNAPSHOT") ? "mrdevopsapp-snapshot" : "mrdevopsapp-release"

        //             nexusArtifactUploader artifacts: 
        //             [
        //                 [
        //                     artifactId: 'springboot',
        //                      classifier: '', 
        //                      file: 'target/Uber.jar',
        //                       type: 'jar'
        //                 ]
        //             ], 
        //                     credentialsId: 'nexus-cred', 
        //                     groupId: 'com.example',
        //                     nexusUrl: '54.173.227.17:8081',
        //                     nexusVersion: 'nexus3',
        //                     protocol: 'http', 
        //                     repository: nexusRepo, 
        //                     version: "${readPomVersion.version}"
        //         }
        //     }
        // }
        stage('docker image building'){
            steps{
                script{
                    sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
                    sh 'docker image tag $JOB_NAME:v1.$BUILD_ID balajinaidu7013/$JOB_NAME:v1.$BUILD_ID'
                    sh 'docker image tag $JOB_NAME:v1.$BUILD_ID balajinaidu7013/$JOB_NAME:latest'
                    
                }
            }
        }

        stage('push image to dokcer hub')
        {
            steps{
                script{
                     withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhubb')]) {
                          sh 'docker login -u balajinaidu7013 -p ${dockerhubb}'
                          sh 'docker image push balajinaidu7013/$JOB_NAME:v1.$BUILD_ID'
                          sh 'docker image push balajinaidu7013/$JOB_NAME:latest'
                    }
                }
            }
        }
        }

}