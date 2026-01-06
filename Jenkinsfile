pipeline{
    // agent {label 'sonar'}
    agent (label 'jfrog')
    stages{
       /*stage('Git Checkout Stage'){
            steps{
                git branch: 'main', url: 'https://github.com/tranju664/Sonar-Qube-war-example.git'
            }
         }*/       
       stage('Build Stage'){
            steps{
                sh 'mvn clean install'
            }
         }
    }
        post {
                success {
                    script {
                        def server = Artifactory.newServer(url: 'http://13.127.163.245:8081/artifactory/', credentialsId: 'jfrog')
                        def rtMaven = Artifactory.newMavenBuild()
                        rtMaven.deployer server: server, releaseRepo: 'libs-release/', snapshotRepo: 'libs-snapshot/'
                        rtMaven.tool = 'maven'
                        rtMaven.run(pom: 'pom.xml', goals: 'clean install')
                    }
                }
            }
    }
