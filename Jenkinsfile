 pipeline {
 environment {
 imagename = "mohammadib/qualcom-web.0405"
 registryCredential = 'mohammadib'
 dockerImage = ''
 }
 agent any
 stages {
 stage('Cloning Git') {
 steps {
 git([url: 'https://github.com/mb0615/jenkinstestmb.git', branch: 'main'])
 }
 }
 stage('Building image') {
 steps{
 script {
 dockerImage = docker.build imagename
 }
 }
 }
 stage('Running image') {
 steps{
 script {
 sh "docker run -itd -P ${imagename}:latest"
 }
 }
 }
 stage('Deploy Image') {
 steps{
 script {
 docker.withRegistry( '', registryCredential ) {
 dockerImage.push("$BUILD_NUMBER")
 dockerImage.push('latest')
 }
 }
 }
 }
 }
}
