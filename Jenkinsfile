pipeline { 

  

    agent any 

  

    tools { 

  

        // Install the Maven version configured as "Maven" and add it to the path. 

  

        maven "3.8.5" 

    } 

    stages { 

  

stage("SCM Checkout"){ 

  

steps{ 

  

checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: <'Credential ID'>, url: <'Git Repo URL’>]]]) 

} 

  

} 

        stage('Build') { 

  

            steps { 

  

                // Run Maven on a Unix agent. 

  

                sh "mvn -Dmaven.test.failure.ignore=true clean package" 

  

                // To run Maven on a Windows agent, use 

  

                // bat "mvn -Dmaven.test.failure.ignore=true clean package" 

  

            } 

  

            post { 

  

                // If Maven was able to run the tests, even if some of the test 

  

                // failed, record the test results and archive the jar file. 

  

                success { 

  

                    archiveArtifacts 'target/*.war' 

  

                } 

  

            } 

  

        } 

  

        stage('Deploy'){ 

steps { 

  

deploy adapters: [tomcat9(credentialsId: <'credential ID'>, path: '', url: <'URL'>)], contextPath: null, war: '**/*.war' 

  

        } 

} 

    } 

} 

  

 
