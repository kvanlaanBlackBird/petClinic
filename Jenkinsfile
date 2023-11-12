pipeline {
    agent any

    environment {
        // Define environment variables if needed
        MAVEN_HOME = tool 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from version control
                checkout main
            }
        }

        stage('Build') {
            steps {
                // Build your Maven project
 		sh '''
                    ./mvnw package
                    java -jar target/*.jar
                '''
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube analysis
                script {
                    def scannerHome = tool 'SonarQubeScanner'
                    withSonarQubeEnv('SonarQubeServer') {
                        sh /bin/sonar-scanner
                    }
                }
            }
        }

            
        
    }

    post {
        success {
            // Actions to take when the build is successful
        }

        failure {
            // Actions to take when the build fails
        }

        unstable {
            // Actions to take when the build is unstable
        }

        always {
            // Actions to take regardless of the build result
        }
    }
}
