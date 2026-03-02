pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh '''
                echo "Building Java project..."
                ls
                cd "Password Protection"
                mkdir -p build
                javac -d build src/*.java
                echo "Build successful"
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                echo "Running Test Stage..."
                cd "Password Protection"

                if [ -d "test" ]; then
                    echo "Test directory found"
                else
                    echo "No tests found — skipping"
                fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Packaging Application..."
                cd "Password Protection"
                jar cf FileEncrypter.jar -C build .
                echo "Deployment successful"
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
