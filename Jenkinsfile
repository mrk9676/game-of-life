pipeline {
    agent { label 'HRMS&&QA' }
    stages {
        stage('git'){
            steps {
                git branch: 'DeclarativePipeline', url: 'https://github.com/dummyrepos/game-of-life.git'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}
