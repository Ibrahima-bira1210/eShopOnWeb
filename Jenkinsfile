pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'dotnet build eShopOnWeb.sln'
      }
    }

    stage('Test') {
      parallel {
        stage('Unit') {
          steps {
            sh 'dotnet test tests/UnitTests'
          }
        }

        stage('Integration') {
          steps {
            warnError(message: 'Functional test probleme') {
              sh 'dotnet test tests/IntegrationTests'
            }

          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet publish eShopOnWeb.sln -o /Users/macbook/Desktop/aspnet'
        dir(path: '//Users/macbook/Desktop/aspnet') {
          archiveArtifacts(onlyIfSuccessful: true, artifacts: '*')
        }

      }
    }

  }
}