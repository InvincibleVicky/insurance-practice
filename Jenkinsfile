pipeline {
    agent any 

    stages {

        stage("git clone"){
            steps{
                echo "cloning git"
                git url: "https://github.com/InvincibleVicky/insurance-practice/"
            }
        }

        stage("compile"){
            steps{
                echo "compliling"
                sh "mvn compile"
            }
        }

        stage("test"){
            steps{
                echo "testing"
                sh "mvn test"
            }
        }

        stage("QA"){
            steps{
                echo "QA checkstyle"
                sh "mvn checkstyle:checkstyle"
            }
        }

        stage("package"){
            steps{
                echo "packaging"
                sh "mvn package"
            }
        }
    }
}
