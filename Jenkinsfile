pipeline {
    agent 'any'
    parameters {
        string(name:'Branch_Name', defaultValue: 'master', description: 'Enter Branch Name')
        choice(name:'Maven_goal',choices: ['package','compile','test','deploy'], description: 'Maven goal')

    }
    stages {
        stage('git') {
        agent { label 'master' }
            steps {
            git url: 'https://github.com/mrk9676/game-of-life.git', branch: 'master'
            }
        }
        stage('maven'){
        agent { label 'master' }
            when { expression { "${Branch_Name}" == 'master'} }
            steps{
                sh '/opt/apache-maven-3.6.3/bin/mvn package'
            }
        }
        stage('archiving results'){
        agent { label 'master' }
            steps{
                junit testResults: 'gameoflife-web/target/surefire-reports/*xml'
                archive includes: 'gameoflife-web/target/*war'

            }
        }
    }   
}
