pipeline{
    agent any

    stages{
        stage('Build'){
            steps{
                script{
                    def nodejstool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    env.PATH = "${nodejstool}/bin:${env.PATH}"
                }
                sh 'echo "Building the application..." '
                sh 'npm install'
                sh 'npm run-script build'
            }
        }
        stage('Docker'){
            steps{
                sh 'echo "Dockerizing the application..." '
            }
        }
        // stage('Build'){
        //     steps{
        //         sh 'echo "Building the application..." '
        //     }
        // }
    }
}