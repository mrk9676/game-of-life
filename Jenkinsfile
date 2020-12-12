pipeline {
    agent { label 'my-node'}
    triggers {
        pollSCM('* * * * *')
    }
    parameters { 
        string(name: 'Branch_name', defaultValue: 'master', description: 'Enter the branch to work on')
        string(name: 'Maven_goal', defaultValue: 'package', description: "Enter the maven goal")
        string(name: "Test_results_path", defaultValue: "gameoflife-web/target/surefire-reports/*xml", description: "Test results Path")
        string(name: "Package_name", defaultValue: "gameoflife-web/target/*war", description: "Package name to display")

  }
  stages {
      stage ('git'){
            steps {
                git url: "https://github.com/mrk9676/game-of-life.git", branch: "${params.Branch_name}"
            }
      }
      stage ('Building tool') {
          steps {
              sh "mvn ${params.Maven_goal}"
          }
      }
      stage ('Publishing test results'){
          steps{
              junit "${params.Test_results_path}"
            
          }
      }
      stage ('Archiving artifacts'){
          steps{
              archive includes: "${params.Package_name}"
          }
      }

  }
}
