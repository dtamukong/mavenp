pipeline
{
    agent any
    stages
    {
        stage('ContinousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/dtamukong/mavenp.git'
                    }
                    catch(Exception e1)
                    {
                       mail bcc: '', body: 'Jenkins is unable to download the development code from github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.team@gmail.com' 
                        exit(1)
                    }
                }
                
            }
        }
        stage('ContinousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                      sh 'mvn package'  
                    }
                    catch(Exception e2)
                    {
                       mail bcc: '', body: 'Jenkins is unable to create an artifact from the downloaded code', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'dev.team@gmail.com'
                        exit(1)
                    }
                }
                
            }
        }
        stage('ContinousDeloyment')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: 'c5b9db0d-318a-4838-86fc-ed04327a81e4', path: '', url: 'http://172.31.13.149:8080')], contextPath: 'Testapp', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                       mail bcc: '', body: 'Jenkins is unable deploy artifact on onto tomcat on the QAServer', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middleware.team@gmail.com' 
                        exit(1)
                    }
                }
               
            }
        }
        stage('ContinousTesting')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/dtamukong/FunctionalTestingProf.git'
       sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Jenkins is unable to test the Selenium scripts from github', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'qa.team@gmail.com'
                        exit(1)
                    }
                }
                

            }
        }
        stage('ContinousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                        input message: 'waiting for approval from DM', submitter: 'shekina'
       deploy adapters: [tomcat9(credentialsId: 'c5b9db0d-318a-4838-86fc-ed04327a81e4', path: '', url: 'http://172.31.0.76:8080')], contextPath: 'Prodapp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the prodserver', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'deleveryteam@gmail.com'
                    }
                }
                

            }
        }
    }
}
