# Declarative_Pipeline
Creating a pipeline with poll scm as a trigger

This is my a pipeline script
pipeline{
    agent{
        label "vinod"
    }
    stages{
        stage("Code"){
            steps{
                echo "This is stage where source code is present means cloning "
                git url : "https://github.com/Mansi-Mishra-2004/Declarative_Pipeline.git",branch:"main"
                echo "code cloning successfully"
            }
        }
        stage("Build"){
            steps{
                echo "This is stage where our docker will run"
                sh "whoami"
                sh "docker build -t notes-app:latest ."
                
            }
        }
        stage("Test"){
            steps{
                echo "This is stage where our windows server have to run"
            }
        }
        stage("Deploy"){
            steps{
                echo "Finally deploying it..WOHOOOO"
                sh "docker run -d -p 8000:8000 notes-app:latest"
                
            }
        }
    }
}
