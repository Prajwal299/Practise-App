pipeline{
    agent any
    stages{
        stage("installation"){
            steps{git branch: 'main', url: 'https://github.com/Prajwal299/Practise-App.git'}
        }
        stage("Docker-built image") {
       steps {
        bat '''
            docker build -t flask-app-11 '''
    }
}
stage("run contasiner") {
    steps {
        bat '''
           docker run -d -p 5000:5000 flask-app-11
        '''
    }
}

    }
    post{
        success{
            echo "successfull"
        }
        failure{
            echo "Failed"
        }
    }
}