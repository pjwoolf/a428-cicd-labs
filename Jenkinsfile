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

node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install' 
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?'
        }
    }
}
