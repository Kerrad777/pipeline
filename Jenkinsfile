pipeline {
    agent any
    parameters {
        string(defaultValue: '', description: 'Student name', name: 'studentName')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                credentialsId: 'b72b54ef-81f8-48fc-8658-836d9fcee8a8',
                url: 'https://github.com/Kerrad777/pipeline.git'
            }
        }
        stage('Build') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Run script') {
            steps {
                sh "python hello.py --name '${params.studentName}'"
            }
        }
        stage('Save output') {
            steps {
                sh 'echo $BUILD_OUTPUT > result.txt'
                archiveArtifacts artifacts: 'result.txt', onlyIfSuccessful: true
            }
        }
        stage('Push to repository') {
            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'b72b54ef-81f8-48fc-8658-836d9fcee8a8', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')
                ]) {
                    sh "git config --global user.email '${GIT_USERNAME}'"
                    sh "git config --global user.name 'Your Name'"
                    sh "git push --set-upstream origin main"
                }
            }
        }
    }
}
