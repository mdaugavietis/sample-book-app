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
                test("BOOKS", "DEV")
            }
        }
        stage('Deploy to STG') {
            steps {
                deploy("STG", 2050)
            }
        }
        stage('Test on STG') {
            steps {
                test("BOOKS", "STG")
            }
        }
        stage('Deploy to PRD') {
            steps {
                deploy("PRD", 3050)
            }
        }
        stage('Test on PRD') {
            steps {
                test("BOOKS", "PRD")
            }
        }
    }
}
def build() {
    echo 'Building of node application is starting..'
    sh "npm install"
    sh "npm test"
}

def deploy(String environment, int port){
    echo "Deployment to ${environment} has started.."
    // Uz nixos pēc darba visi konvejiera čaulas darbi tiek notīrīti
    // sh "pm2 delete \"books-${environment}\""
    git branch : 'main', poll: false, url: 'https://github.com/mdaugavietis/sample-book-app' 
    sh "npm install"
    sh "pm2 start -n \"books-${environment}\" index.js -- ${port}"
}

def test(String testSet, environment){
    echo "Testing  ${testSet} test set on ${environment} has started.."
    git branch : 'main', poll: false, url: 'https://github.com/mdaugavietis/api-automation' 
    sh "npm install"
    sh "npm run ${testSet} ${testSet}_${environment}"
}
