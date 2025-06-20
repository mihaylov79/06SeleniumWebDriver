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

        stage('Install Google Chrome') {
            steps {
                sh '''
                wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
                sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
                sudo apt-get update
                sudo apt-get install -y google-chrome-stable
                '''
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
                sh 'dotnet test TestProject1/TestProject1.csproj' 
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