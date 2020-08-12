pipeline {
    agent any

    stages {
        
        stage('Docker Build'){
            steps{
                bash(script: 'docker images -a')
                bash(script: """
                    cd azure-vote/
                    docker images -a
                    docker build -t jenkins-pipeline .
                    docker images -a
                    cd ..
                    """)
            }
        }
    }
}