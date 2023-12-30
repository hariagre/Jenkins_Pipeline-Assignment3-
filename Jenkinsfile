pipeline {
    agent any

    stages {
        stage('Test') {
            when {
                expression { return env.BRANCH_NAME == 'develop' }
            }
            steps {
                // Checkout code from Git
                script {
                    checkout scm
                }

                // Trigger the 'test' job
                build job: 'test'
            }
        }

        stage('Production') {
            when {
                expression { return currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                // Checkout code from Git
                script {
                    checkout scm
                }

                // Trigger the 'prod' job
                build job: 'prod'
            }
        }
    }
}
