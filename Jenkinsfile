pipeline {
    agent any

    stages {
        stage('build') {
            steps {
              build()
            }
        }
        stage('Deploy to DEV') {
            steps {
                deploy("DEV")
            }
        }
        stage('Test on DEV') {
            steps {
                test("DEV")
            }
        }
        stage('Deploy to STG') {
            steps {
                deploy("STG")
            }
        }
        stage('Test on STG') {
            steps {
                test("DEV")
            }
        }
        stage('Deploy to PRD') {
            steps {
                deploy("PRD")
            }
        }
        stage('Test on PRD') {
            steps {
                test("DEV")
            }
        }
    }
}
def build() {
    echo 'Building of node application is starting..'
}

def deploy(String environment){
    echo "Deployment to ${environment} has started.."
}

def test(String environment){
    echo "Testing on ${environment} has started.."
}
