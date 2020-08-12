pipeline {
    agent any

    stages {
        
        stage('Docker Build'){
            steps{
                pwsh(script: 'docker images -a')
                pwsh(script: """
                    cd azure-vote/
                    docker images -a
                    docker build -t jenkins-pipeline .
                    docker images -a
                    cd ..
                    """)
            }
        }
        stage('start test app'){
            steps{
                pwsh(script:"""
                # start app line missing
                ./scripts/test_container.pwsh
                """)
            }
            post{
                success{
                    echo "app started successfully :)"
                }
                failure{
                    echo "app failed to start :("
                }
            }
            
        }
        stage('Run Tests'){
            steps{
                pwsh(script: """
                 pytest ./tests/test_sample.pwsh
                """)
            }
        }
        stage('Stop test app'){
            steps {
                pwsh(script: """
                docker-compose down
                """)
            }
        }
    }
}