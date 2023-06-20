// node {
//     checkout scm
//     docker.image('node:16-buster-slim').inside('-p 3000:3000') {
//         stage('Build') {
//             sh 'npm install' 
//         }
//         stage('Test') {
//             sh './jenkins/scripts/test.sh'
//         }
//         stage('Manual Approval') {
//             input message: 'Lanjutkan ke tahap Deploy?'
//         }
//         stage('Build Image') {
//             withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
//                 sh 'docker build -t jennykibiri/sample-react-app .'
//                 sh "echo $PASS | docker login -u $USER --password-stdin"
//                 sh 'docker push jennykibiri/sample-react-app'
//             }
//         }
//         stage ('Deploy') {
//             script {
//                 def dockerCmd = 'docker run  -p 3000:3000 -d jennykibiri/sample-react-app:latest'
//                 sshagent(['ec2-server-key']) {
//                     sh "ssh -o StrictHostKeyChecking=no ec2-user@3.92.144.96 ${dockerCmd}"
//                 }
//             }
//         }
//     }
// }

pipeline {
    agent any
    tools {
        nodejs 'nodejs'
    }
    parameters {
        choice(name:'VERSION', choices:['1.0', '1.1', '1.2'], description:'Choose the version of the project')

        booleanParam(name :'executeTests', description:'Execute the tests', defaultValue:false)
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                // sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                // sh 'npm run test'
                echo "Test"

            }
        }
        stage('Build Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'docker build -t elvirareza/sample-react-app .'
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push elvirareza/sample-react-app'
                }
            }
        }
        stage ('Deploy') {
            steps {
                script {
                    def dockerCmd = 'docker run  -p 3000:3000 -d elvirareza/sample-react-app:latest'
                    sshagent(['ec2-server-key']) {
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@54.179.7.244 ${dockerCmd}"
                    }
                }
            }
        }
    }
}