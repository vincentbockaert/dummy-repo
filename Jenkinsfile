pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "Building from a feature branch"'
            }
        }
    }

    post {
        always {
            script {
                if (env.BRANCH_NAME == 'main') {
                    // Do not purge builds for the main branch
                    currentBuild.getRawBuild().getParent().logRotator = new hudson.tasks.LogRotator(-1, 5, -1, -1)
                } else {
                    // Keep builds for 5 days for other branches
                    // int daysToKeep, int numToKeep, int artifactDaysToKeep, int artifactNumToKeep
                    currentBuild.getRawBuild().getParent().logRotator = new hudson.tasks.LogRotator(-1, 3, -1, -1)
                }
            }
        }
    }
}
