pipeline{
    agent any

    environment{
        // CHROME_VERSION = '137.0.7151.69'
        CHROMEDRIVER_VERSION = '137.0.7151.69'
        // CHROME_INSTALL_PATH = ''
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
                sh 'dotnet test TestProject1/TestProject.csproj' 
            }
        }


    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}