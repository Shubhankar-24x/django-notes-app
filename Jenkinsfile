@Library("Shared") _

pipeline{
    
    agent{label "tyson"}
    
    stages{
        
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        
        stage("CodeClone"){
            steps{
                script{
                    clone("https://github.com/Shubhankar-24x/django-notes-app.git", "dev")
                }
            }
        }
        
        stage("Build"){
            steps{
                script{
                    docker_build("notesapp","latest","shubhankar24")
                }
                
            }
        }
        
        stage("Test"){
            steps{
                echo "This is testing"
            }
        }
        
        stage("Push to DockerHub"){
            steps{
                script{
                    docker_push("notesapp","latest","shubhankar24")
                }
            }
        }
        
        stage("Deploy"){
            steps{
                script{
                    docker_compose()
                }
            }
        }
        
    }
}
