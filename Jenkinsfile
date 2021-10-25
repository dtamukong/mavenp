pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload_Loans')
        {
            steps
            {
                script
                {
                    try
                    {
                         git 'https://github.com/intelliqittrainings/maven.git'
                    }
                    catch(Exception e1)
                    {
                        
                        mail bcc: '', body: 'Jenkins is unable to download from the remote github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.admin@gmail.com'
                        exit(1)
                    }
                }
               
            }
        }
}
}
