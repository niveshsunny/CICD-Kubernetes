def COLOR_MAP = [   // Slack notification color
    'SUCCESS': 'good',
    'FAILURE': 'danger',
]
pipeline {
    agent any
    
    tools {
        maven "MAVEN3"
        jdk "OracleJDK11"
    }
     environment {
        registry = "niveshsunny/vproapp"
        registryCredential = 'dockerhub'

 
    }
    stages {
    
        stage('UNIT TEST') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Checkstyle Analysis') {  // checkstyle to scan your code aginest best practices, bugs and vulunerbilities 
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
        
        stage('Sonar Analysis') { //scan the code and upload result to sonarqube scanner server
            environment {
                SCANNER_HOME = tool 'sonar4.7'
            }
            steps {
                withSonarQubeEnv('sonar') { // environment name is in configure system & below variables are used to mention path of the src code
                    sh "${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                        -Dsonar.projectName=vprofile-repo \
                        -Dsonar.projectVersion=1.0 \
                        -Dsonar.sources=src/ \
                        -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                        -Dsonar.junit.reportsPath=target/surefire-reports/ \
                        -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                        -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml"
                }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {  // Set a timeout for the quality gate check // sonar will send the result to jenkins using webhooks (pass/fail)
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        

        stage('Build App Image') {
            steps {
       
         script {
                dockerImage = docker.build registry + ":$BUILD_NUMBER"
             }

     }
    
    }

    stage('Upload App Image') {
          steps{
            script {
                docker.withRegistry('', registryCredential){ //docker.withRegistry is function with credentials its going to psuh image to docker hub
                    dockerImage.push("$BUILD_NUMBER")
                    dockerImage.push("latest")
                }

            }
          }
     }
     stage('Remove unused Docker Image') {
          steps{
            sh "docker rmi $registry:$BUILD_NUMBER"
          }
     }
     stage('Update Deployment File') {
        environment {
            GIT_REPO_NAME = "CICD-Kubernetes"
            GIT_USER_NAME = "niveshsunny"
        }
        steps {
            withCredentials([string(credentialsId: 'github', variable: 'GITHUB_TOKEN')]) {
                sh '''
                    git config user.email "niveshreddy963@gmail.com"
                    git config user.name "niveshsunny"
                    BUILD_NUMBER=${BUILD_NUMBER}
                    sed -i "s/Imagetag/${BUILD_NUMBER}/g" template/vproappdeb.yml
		    cp -f vproappdeb.yml ../helm/vprofilecharts/templates/vproappdeb.yml
                    git add .
                    git commit -m "Update deployment image to version ${BUILD_NUMBER}"
                    git push https://${GITHUB_TOKEN}@github.com/${GIT_USER_NAME}/${GIT_REPO_NAME} HEAD:main
                '''
            }
        }
    }

    //  stage('Deploy to Kubernetes') {
    //     agent {label 'KOPS'}
    //       steps{
    //         sh "helm upgrade --install --force vprofile-stack /home/ubuntu/vprofile-project/helm/vprofilecharts --set appimage=${registry}:${BUILD_NUMBER}"
    //       }
    //  }
    

    }
post {
    always {
        script {
            // Determine color based on build result
            def color = COLOR_MAP[currentBuild.currentResult] ?: 'warning'
            // Send message to Slack channel with dynamic color
            slackSend(channel: '#jenkinscicd', color: color, message: "*${currentBuild.currentResult}:* Build '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL}) ${currentBuild.currentResult}")
        }
    }
}
}

