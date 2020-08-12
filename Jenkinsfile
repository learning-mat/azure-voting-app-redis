pipeline {
    agent any

    stages {
        
        stage('Docker Build'){
            steps{
                powershell (script: 'docker images -a')
                powershell (script: """
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
                powershell (script:"""
                # start app line missing
                ./scripts/test_container.ps1
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
                powershell (script: """
                 pytest ./tests/test_sample.ps1
                """)
            }
        }
        stage('Stop test app'){
            steps {
                powershell (script: """
                docker-compose down
                """)
            }
        }
    }
}