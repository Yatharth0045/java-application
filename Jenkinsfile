pipeline
{
    agent {
        label 'Development'
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
        stage("Compile")
        {
            steps{
                sh 'mvn compile'
            }
        }
        
        stage("Test")
        {
        
            steps
            {
                sh 'mvn test'
            }
        }
        stage("Package")
        {
            steps{
                sh 'mvn package'
            }
        }
    }
    post
    {
        always
        {
                emailext (attachLog: true, body: '$DEFAULT_CONTENT', subject: '$DEFAULT_SUBJECT', to: 'dipayan.pramanik@knoldus.com')  
        }
        success{
            archiveArtifacts artifacts: "**/*.jar"
        }
    }
}