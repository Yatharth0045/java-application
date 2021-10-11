pipeline
{
    agent {
        label 'Testing'
    }
    tools
    {
        maven 'mvn'
        jdk 'Java'
    }
    options
    {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
    }
    stages
    {
        stage("Cleanup")
        {
            steps
            {
                sh 'mvn clean'
            }
        }
        
        stage("Test")
        {
            steps
            {
                sh 'mvn test'
            }
        }
    }
    post
    {
        always
        {
                emailext (attachLog: true, body: '$DEFAULT_CONTENT', subject: '$DEFAULT_SUBJECT', to: 'dipayan.pramanik@knoldus.com')  
        }
    }
}