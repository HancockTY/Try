pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
/*     stage ('Check-Git-Secrets') {
    steps {
      sh 'rm trufflehog || true'
      sh 'docker run gesellix/trufflehog --json https://github.com/HancockTY/Try.git > trufflehog'
      sh 'cat trufflehog'
    }
  } 
    
   stage ('Source Composition Analysis') {
    steps {
      sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
       sh 'chmod +x owasp-dependency-check.sh'
     sh 'bash owasp-dependency-check.sh'
     sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        
     }
  } */
    
   stage ('SAST') {
     steps {
      withSonarQubeEnv('sonar') {
      sh 'mvn sonar:sonar'
     sh 'cat target/sonar/report-task.txt'
      }
   }
   } 
    
 /*  stage ('Build') {
      steps {
     sh 'mvn clean package'
    
       }
    }         */
    
  /* stage ('Deploy-To-Tomcat') {
           steps {
          echo 'deploy'
          }       
   }             */
    
    
  stage ('DAST') {
      steps {
       sshagent(['zap']) {
        // sh 'ssh -o  StrictHostKeyChecking=no ubuntu@13.232.158.44 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://13.232.202.25:8080/webapp/" || true'
         //sh 'docker run -t owasp/zap2docker-stable zap-baseline.py -t http://ec2-18-221-251-162.us-east-2.compute.amazonaws.com:8080/" || true'
         sh 'docker run -t owasp/zap2docker-stable zap-baseline.py -t http://18.117.153.231:8080/webapp/ || true'
       }
      }
    }  

    
  }
}
