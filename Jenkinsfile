pipeline {

    tools {
        jdk 'jdk17'
        nodejs 'node16'

    }
    environment{
        def scannerHome = tool 'SonarScanner 4.0';
        def imageRegistry = '' ;
        def image = '' ;
    }

    stages {
        // git checkout from repository
        stage('Git checkout') {
            steps {
                git branch: 'master', url: ''                
            }
        }

        // git checkout from repository
        stage('Sonarqube analysis') {
            steps {                
                withSonarQubeEnv('My SonarQube Server') {         
                sh '''${scannerHome}/bin/sonar-scanner <code_goes here>

                '''
              }
            }
        }
   
        stage('Quality gates') {
            STEPS { 
                waitForQualityGate abortPipeline: false
            }
        }

        stage('Install DP') {
            steps {
                echo 'intalling dependency'
                sh 'npm install'

            }
        }

        stage('OWASP DP-Check') {
            steps {
               echo 'performing OWASP dependency check for vulnerabilities'
            }
        }
   
        stage('Trivy file scan') {
            steps {
                echo 'running trivy file scan and saving report to trivyfsreport.txt'
                sh 'trivy fs . >> trivyfsreport.txt'
            }
        }
        stage('Build Image') {
            steps {
               echo 'building docker image for the app' 
               sh 'docker build --buld-args ( cat .env | xargs )-t $imageRegistry/$image .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                echo 'login and push to docker registry'
            }
        }

        stage('Trivy Image scan') {
            steps {
                echo 'running trivy image scan and saving report to trivyimagereport.txt'
                sh 'trivy image $image >> trivyimagereport.txt'
            }
        }
   
        stage('Deploy to docker') {
            steps {
                echo 'deeploying to docker on port 8080'
                sh 'docker run -d -rm -p 8080:80'
            }
        }

        stage('Deploy to k8s') {
            steps {
                sh 'kubectl'
            }
        }
   
        
    }
}