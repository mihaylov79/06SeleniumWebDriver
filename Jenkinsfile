pipeline{
    agent any

    environment{
        CHROMEDRIVER_VERSION = '137.0.7151.69'
        CHROMEDRIVER_PATH = '/usr/local/bin/chromedriver'
    }


    stages{
        stage("Checkout code"){
            steps{
                git branch: 'main', url: 'https://github.com/mihaylov79/06SeleniumWebDriver.git' 
            }

        }



        stage("Installing Dependancies"){
            steps{
                sh 'dotnet restore'
            }
           
        }

        stage("Building App"){
            steps{
                sh 'dotnet build --configuration release'
            }
            
        }

        stage("Testing TestProject1"){
            steps{
                sh 'echo Testing TestProject1'
                sh 'dotnet test TestProject1/TestProject1.csproj --no-build || true' 
            
                
                sh 'echo Testing TestProject2'
                sh 'dotnet test TestProject2/TestProject2.csproj --no-build --logger:"trx;LogFileName=TestResults.trx" || true' 
            
                sh 'echo Testing TestProject3'
                sh 'dotnet test TestProject3/TestProject3.csproj --no-build --logger:"trx;LogFileName=TestResults.trx" || true' 

            
            }
        }


    }
    post{
        always{
            echo "===== always ====="
            archieveArtifacts artfacts: '**/TestResults.trx', allowEmptyArchive: true
            junit '**/TestResults.trx'
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}