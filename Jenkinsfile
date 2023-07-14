node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        
        }
        stage('Deploy') {
                sh './jenkins/scripts/deliver.sh'
                input(
                    message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)',
                    parameter: [
                        [$class: 'ChoiceParameterDefinition', name:'userInput', choices: ['Proceed', 'Abort']]
                    ]
                )
                if (userInput == 'Proceed') {
                sh './jenkins/scripts/kill.sh'
                } else {
                    error('Pipeline aborted by user')
                }            
        }
    }
}