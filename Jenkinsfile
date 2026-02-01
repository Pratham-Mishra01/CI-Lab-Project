pipeline {
    agent any

    stages {

        stage('Identify Branch') {
            steps {
                echo "Current branch is: ${env.BRANCH_NAME}"
            }
        }

        stage('Main Branch CI') {
            when {
                expression { env.BRANCH_NAME == 'main' }
            }
            steps {
                echo 'Executing full build on main branch'
                bat 'scripts\\build.bat'
            }
        }

        stage('Feature Branch Validation') {
            when {
                expression { env.BRANCH_NAME.startsWith('feature/') }
            }
            steps {
                echo 'Executing lightweight checks for feature branch'
                bat 'python scripts\\hello.py'
            }
        }

        stage('Release Branch Checks') {
            when {
                expression { env.BRANCH_NAME.startsWith('release/') }
            }
            steps {
                echo 'Performing pre-release validation steps'
            }
        }
    }
}
