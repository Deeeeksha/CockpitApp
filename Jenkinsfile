pipeline{
    agent any
    options{
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment{
        
        image_tag='docker.pkg.github.com/deeeeksha/cockpitapp/cockpitapp:${GIT_COMMIT}'
        cred=credentials('cockpitcred')
        
    }
    
    stages{
        
       
        stage("Packaging, pushing to DockerHub and deploying to Kubernetes Cluster")
        {
            steps{
                sh "docker build -t $image_tag ."
            }
        }
        stage("push image to github repo")
        {
            steps{
                sh """ 
                echo $cred_PSW | docker login docker.pkg.github.com -u $cred_USR --password-stdin 
                docker push $image_tag
                """
            } 
        }
    }
}