pipeline {
    agent { label "Slave_1" }
    
    triggers {
        pollSCM('* * * * *')
    }    

    stages {
        stage('clone_project_A') {
            steps {
                echo 'clone project A'
                git branch: 'main', url: 'https://github.com/Manjunath-Cloud/Hello-world_latest.git'
            }
        }
        stage('build_project_A') {
            steps {
                echo 'build_projectA'
                sh 'yum install maven -y'
                sh 'mvn clean package'
            }
        } 
        stage('Docker_build') {
            steps {
                echo 'Docker build_project03'
                sh 'docker build -t project03 .' 
            }
        }
        stage('login to dockerhub') {
            steps {
                echo 'login to dockerhub'
                sh 'docker login -u manjunathr03 -p Manja@8971'
            }
        } 
        stage('Tag the Image') {
            steps {
                echo 'Tag the Image'
                sh 'docker tag  project03 manjunathr03/project03'
            }
        } 
        stage('Deploy to docker hub') {
            steps {
                echo 'Deploy to docker hub'
                sh 'docker push manjunathr03/project03'
            }
        }
        stage('Remove Docker conatiner') {
            steps {
                echo 'Remove Docker conatiner'
                sh 'docker stop projectd_conatiner || true'
                sh 'docker rm projectd_conatiner || true'
            }
        }        
        stage('Run docker image') {
            steps {
                echo 'Deploy to docker hub'
                sh 'docker run --name project03_conatiner -d -p 9090:8080 manjunathr/project03'
            }
        }       
    }
}
