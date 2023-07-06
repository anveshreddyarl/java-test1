pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build'
                sh 'mvn clean install -e'
                sh 'mvn package'
            }
        }
        stage ('SonarQube analysis') {
            steps {
                 withSonarQubeEnv(installationName:'sonar',credentialsId:'sonar'){
                            sh 'mvn sonar: sonar -Dsonar.projectKey=chalasanil -Dsonar. organization=chalasanil'
                            
                            }
                        }
                    }
        stage('Quality gate') {
            steps {
                timeout(time: 10, unit: 'MINUTES') {
                    script {
                         try {
                            waitForQualityGate abortPipeline: true
                             } catch (Exception ex) {
                                            // Handle any exceptions or errors here
                                            }
                                       }
                                }
                        }
                }
        }
}