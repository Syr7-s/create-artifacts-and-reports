pipeline {
    agent any
    tools {
      maven 'Maven'
    }
    stages {
        stage('Source') {
            steps {
                sh 'mvn --version'
                git branch: 'devisa',
                    changelog: false,
                    poll: false,
                    url: 'https://github.com/Syr7-s/create-artifacts-and-reports.git'
            }
        }
        stage('Clean') {
            steps {
                dir("${env.WORKSPACE}"){
                    echo "Cleaning the workspace..."
                    // Uncomment the following line after Maven is configured as a global tool
                    sh 'mvn clean'
                }
            }
        }
        stage('Test') {
            steps {
                dir("${env.WORKSPACE}"){
                    echo "Running tests..."
                    // Uncomment the following line after Maven is configured as a global tool
                    sh 'mvn test'
                }
            }
        }
        stage('Package') {
            steps {
                dir("${env.WORKSPACE}"){
                    echo "Creating the JAR file..."
                    // Uncomment the following line after Maven is configured as a global tool
                    sh 'mvn package -DskipTests'
                }
            }
        }
    }
    post {
        always {
            echo "Collecting jUnit test results..."
            // Add jUnit report collection here...
            junit allowEmptyResults: true,
                testResults: '**/TEST-com.learningjenkins.AppTest.xml'

            echo "Archiving the JAR file..."
            // Add artifact archiving here...
            archiveArtifacts allowEmptyArchive: true,
                artifacts: '**/hello-1.0-SNAPSHOT.jar',
                fingerprint: true,
                followSymlinks: false,
                onlyIfSuccessful: true
            
        }
    }
}
