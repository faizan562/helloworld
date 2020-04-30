def remote = [:]
remote.host = "40.117.36.137"
remote.allowAnyHosts = true
remote.name = 'test'
remote.user = 'sadmin'
remote.password = 'Adm@123$$%#'

pipeline {
    options {
        disableConcurrentBuilds()  
    }
    agent any
    stages {
        stage('Git Checkout Project') {
            steps {
                sshCommand remote: remote, command: "rm -rf helloworld"
                sshCommand remote: remote, command: "git clone https://github.com/faizan562/helloworld -b master"
            }      
        }
        stage('Build the Project') {
            steps {
                sshCommand remote: remote, command: "dotnet build helloworld/HelloWorld.sln --configuration Release"
            }      
        }
        stage('Deploy the Project') {
            steps {
                sshCommand remote: remote, command: "systemctl restart hello-world.service", sudo :true
            }      
        }
    }
}
