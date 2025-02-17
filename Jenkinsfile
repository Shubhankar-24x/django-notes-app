@Library("Shared") _

pipeline{

    agent any

    environment{
        SONAR_HOME= tool "sonar"
        
    }

    parameters {
        string(name: 'FRONTEND_DOCKER_TAG', defaultValue: '', description: 'Setting docker image for latest push')
        string(name: 'BACKEND_DOCKER_TAG', defaultValue: '', description: 'Setting docker image for latest push')
    }
    
    stages {
        stage("Validate Parameters") {
            steps {
                script {
                    if (params.FRONTEND_DOCKER_TAG == '' || params.BACKEND_DOCKER_TAG == '') {
                        error("FRONTEND_DOCKER_TAG and BACKEND_DOCKER_TAG must be provided.")
                    }
                }
            }
        }

    stages{
        stage("Introduction"){
            steps{
                echo "This is Notes app with DevSecOps pipeline Configuration"
            }
        }
    }

        stage("Workspace Cleanup"){
            steps{
                script{
                    echo "Cleaning the Workspace Before Proceeding"
                    cleanWs()
                } 
            }
        }
        stage("Git: Code Clone"){
            steps{
                script{
                    clone("https://github.com/Shubhankar-24x/django-notes-app.git","dev")
                }
            }
        }

        stage("Trivy: Filesysytem Scanning"){
            steps{
                script{
                    trivy_scan()
                }
            }
        }

        stage("OWASP : Dependency Check"){
            steps{
                script{
                    owasp_dependency_check()
                }
            }
        }

        stage("Sonarqube: Code Analysis"){
            steps{
                script{
                    sonarqube_analysis("Sonar","notes-app","notes-app")
                }
            }
        }

        stage("SonarQube: Code Quality Gates"){
            steps{
                script{
                    sonarqube_code_quality()
                }
            }
        }

        stage("Docker: Build Images"){
            steps{
                script{

                    dir('django-notes-app/nginx'){
                        sh "docker build -t nginx:latest ."
                    }

                    dir ('django-notes-app/mynotes'){
                        sh "docker build -t mysql:latest ."
                    }

                    dir ('django-notes-app'){
                        docker_build()
                    }
                }
            }
        }





}
        
