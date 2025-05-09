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

        stage("docker image creation"){
            steps{
                sh "docker build -t vigneshwar1908/insurance-practice:v1 ."
            }
        }

        stage("docker login"){
            steps{
                 withCredentials([usernamePassword(credentialsId: 'dockerlogin', passwordVariable: 'dockerpass', usernameVariable: 'dockeruser')]) {
                sh 'docker login -u ${dockeruser} -p ${dockerpass}'                                                       }
            }
        }

        stage("docker push image"){
            steps{
                sh "docker push vigneshwar1908/insurance-practice:v1"
            }
        }

        stage("run"){
            steps{
                ansibleplaybook credentialsId: 'ansible-ssh',
                installation: 'ansible',
                inventory: '/etc/ansible/hosts', 
                playbook: 'ansible-playbook.yml', vaultTmpPath: ''
            }
        }
    }
}
