@Library('my-shared-lib') _

pipeline {
    agent any

    stages {

        stage('Identify Branch') {
            steps {
                script {
                    echo "Building branch: ${env.BRANCH_NAME}"
                }
            }
        }

        stage('Build') {
            when {
                anyOf {
                    branch 'main'
                    expression { env.BRANCH_NAME.startsWith('feature/') }
                }
            }
            steps {
                echo "Running basic build for branch: ${env.BRANCH_NAME}"
                sh 'echo "Running build..."'
            }
        }

        stage('Tests (Main Only)') {
            when {
                branch 'main'
            }
            steps {
                echo "Running full tests from shared library"
                runTests()    // shared library function
            }
        }

        stage('Deploy (Main Only)') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying using shared library..."
                deployApp("prod")
            }
        }
    }
}
