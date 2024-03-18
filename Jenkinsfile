pipeline {
    environment {
          AWS_ACCESS_KEY_ID     = credentials('creds')
          AWS_SECRET_ACCESS_KEY = credentials('creds')
          email_recipients      = ''
    }
    agent {label 'terraform'}
    stages {
      stage ('Check running instances') {
        steps {
          script {
            def runninginstances = sh(script: 'aws ec2 describe-instances --filter "Name=instance-state-name,Values=running" --query "Reservations[*].Instances[*].[InstanceId]" --output text', returnStdout: true).trim().split()
            def instanceCount = runninginstances.size()
            echo "Number of running instances: $instanceCount"
            if (instanceCount > 1) {
                    emailext to: '',
                    subject: "High no. of running instances detected",
                    body: "There are currently ${instanceCount} running instances"
            }
          }
        }
      }
    }
}
    
