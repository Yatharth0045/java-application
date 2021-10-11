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
            agent{
                label 'Testing'
            }
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
            emailext (attachLog: true, body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS: 
            
            Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'dipayan.pramanik@knoldus.com')
            
        }
    }
}