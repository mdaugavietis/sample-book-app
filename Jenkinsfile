pipeline {
    agent any
    triggers {
      pollSCM('*/1 * * * *')
    }
    stages {
        stage('build') {
            steps {
                script {
                  build()
                }
            }
        }
        stage('Deploy to DEV') {
            steps {
                deploy("DEV", 1050)
            }
        }
        stage('Test on DEV') {
            steps {
                test("DEV")
            }
        }
        stage('Deploy to STG') {
            steps {
                deploy("STG", 2050)
            }
        }
        stage('Test on STG') {
            steps {
                test("STG")
            }
        }
        stage('Deploy to PRD') {
            steps {
                deploy("PRD", 3050)
            }
        }
        stage('Test on PRD') {
            steps {
                test("PRD")
            }
        }
    }
}
def build() {
    echo 'Building of node application is starting..'
    sh "ls"
    sh "npm install"
    sh "npm test"
}

def deploy(String environment, int port){
    echo "Deployment to ${environment} has started.."
    // Uz nixos pēc darba visi konvejiera čaulas darbi tiek notīrīti
    // sh "pm2 delete \"books-${environment}\""
    sh "pm2 start -n \"books-${environment}\" index.js -- ${port}"
}

def test(String environment){
    echo "Testing on ${environment} has started.."
}
