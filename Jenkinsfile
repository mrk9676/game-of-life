pipeline {
    agent { label 'HRMS&&QA' }
    triggers { cron('30 * * * 1-5') }
    parameters {
        string(
            name: 'TestResultsPath', 
            defaultValue: 'gameoflife-web/target/surefire-reports/*.xml', 
            description: 'Test Results Path'
        )

        string(
            name: 'ArtifactsToBeArchive',
            defaultValue: 'gameoflife-web/target/*.war',
            description: 'This is archival path'
            
        )

        choice(
            name: 'BranchToBuild',
            choices: ['DeclarativePipeline', 'ScriptedPipeline', 'master'],
            description: 'Branch to be build'

        )
    }
    stages {
        stage('git'){
            steps {
                git branch: "${params.BranchToBuild}", url: 'https://github.com/dummyrepos/game-of-life.git'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('postbuild') {
            steps {
                // junit test Results
                junit testResults: "${params.TestResultsPath}"

                // archive the artifacts
                archive includes: "${params.ArtifactsToBeArchive}"
            }
        }
    }
}
