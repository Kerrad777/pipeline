pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                          branches: [[name: 'main']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [],
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/Kerrad777/pipeline.git']]
                       ])
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        
        stage('Run hello.py') {
            steps {
                sh 'python hello.py -n "Yura" > result.txt'
            }
        }
        
        stage('Publish Artifact') {
            steps {
                archiveArtifacts 'result.txt'
            }
        }
    }
}
