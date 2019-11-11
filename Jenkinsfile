  
pipeline {
agent any

   stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/karim007/dotnet-core-web.git', branch: 'master'
            }
        }
        stage('build') {
            steps {
                sh "dotnet build --configuration Release src/web/dotnet_core_hello_world.csproj"
            } 
        }

        stage('test') {
            steps {
                sh "dotnet test src/test/test.csproj"
            }
        }
        stage("create artefact and push it") {
            steps {
                sh "dotnet publish src/app/dotnet_core_hello_world.csproj --no-build --no-restore --configuration Release -o Artifacts "
            } 
        }

        stage("deploy container"){
            steps {

            ansiblePlaybook(
		        playbook: 'create-web-app.yml'
               )
            } 
               
        } 


    }
}
