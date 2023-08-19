pipeline {
    agent any
    triggers {
        pollSCM '*/3 * * * *'
    }
    parameters {
        string(defaultValue: '', description: 'Student name', name: 'studentName')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([
                  $class: 'GitSCM',
                  branches: [[name: 'main']],
                  userRemoteConfigs: [[
                    url: 'https://github.com/Kerrad777/pipeline.git',
                    credentialsId: 'b72b54ef-81f8-48fc-8658-836d9fcee8a8'
                  ]],
                  skipDefaultCheckout: true
                ])
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
                sh 'mkdir -p output && echo $BUILD_OUTPUT > output/result.txt'
                sh 'git config --global user.email "Kerrad777@yandex.ru"'
                sh 'git config --global user.name "Yura"'
                sh 'git add output/result.txt'
                sh 'git commit -m "Add result.txt"'
            }
        }
        stage('Push to repository') {
            steps {
                sh sh 'git push --set-upstream origin main'
            }
        }
    }
}
