pipeline {
        environment {
     sandbox_Deploy_Path = "C:\\Application\\Sandbox"
     production_Deploy_Path = "C:\\Application\\Production"
        }
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                script {
                    git branch: 'main',
                        url: 'https://github.com/adithyak21/test-angular-project.git'
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    bat"npm install"
                    bat"npm run ng -- build"
                    echo"Angular app built successfully"
                    
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    bat"npm run ng test -- --watch=false --code-coverage"
                    echo"Test completed"
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                  if(BRANCH_NAME=="dev"){
                bat" IF exist ${sandbox_Deploy_Path} ( echo ${sandbox_Deploy_Path} exists ) ELSE ( mkdir ${sandbox_Deploy_Path} && echo ${sandbox_Deploy_Path} created)"
                bat"MOVE ${WORKSPACE}\\dist\\test\\* ${sandbox_Deploy_Path}"
                  }
                    if(BRANCH_NAME=="main"){
                bat" IF exist ${production_Deploy_Path} ( echo ${production_Deploy_Path} exists ) ELSE ( mkdir ${production_Deploy_Path} && echo ${production_Deploy_Path} created)"
                bat"MOVE ${WORKSPACE}\\dist\\test\\* ${production_Deploy_Path}"
                  }
                }
            }
        }
    }
}
