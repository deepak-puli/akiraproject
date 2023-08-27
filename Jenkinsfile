pipeline {
    agent {
        node {
            label 'maven'
        }
        
    }
environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
}
    stages {
        stage("build") {
            steps {
                echo "-------build started-------"
                sh 'mvn clean deploy'
                echo "-------build completed-----"
            }
        }
    stage ("test") {
        steps{
            echo "-------unit test started------"
            sh 'mvn surefire-report:report'
            echo "-------unit test completed----"
        }
    }    
    stage('SonarQube analysis') {
    environment {    
      scannerHome = tool 'valaxy-sonar-scanner'
    }
    steps{
    withSonarQubeEnv('sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
      sh "${scannerHome}/bin/sonar-scanner"
    }
    }
  }
  
}
}
