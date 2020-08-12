pipeline {
    agent any

    stages {
        
        stage('Docker Build'){
            steps{
                sh(script: 'docker images -a')
                sh(script: """
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
                sh(script:"""
                # start app line missing
                ./scripts/test_container.sh
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
                sh(script: """
                 pytest ./tests/test_sample.sh
                """)
            }
        }
        stage('Stop test app'){
            steps {
                sh(script: """
                docker-compose down
                """)
            }
        }
    }
}