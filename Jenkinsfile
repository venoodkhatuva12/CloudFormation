pipeline {

    agent {
        label 'ANY'
    }

    parameters {
        choice(name: 'ACTION', choices:"create\nupdate\ndelete", description:'Select the action')
    }

    stages {
     
        stage('create') {
            when {
                    equals expected: 'create', actual: env.ACTION
            }
            steps{
                sh """
                # Automation for Running the CF Script from Jenkins or local
                CREDS=\$(aws sts assume-role --role-arn arn:aws:iam::123456789000:role/devops-role --role-session-name my-sls-session --out json)
                export AWS_ACCESS_KEY_ID=\$(echo \$CREDS | jq -r '.Credentials.AccessKeyId')
                export AWS_SECRET_ACCESS_KEY=\$(echo \$CREDS | jq -r '.Credentials.SecretAccessKey')
                export AWS_SESSION_TOKEN=\$(echo \$CREDS | jq -r '.Credentials.SessionToken')

                cd applicaitonlb-cloudformation

                aws cloudformation validate-template --region us-east-1 --template-body file://applicaitonlb.json

                aws cloudformation create-stack --stack-name applicaitonlb-cloudformation --region us-east-1 --template-body file://applicaitonlb.json --capabilities CAPABILITY_NAMED_IAM --parameters file://parameters.json
                """
               }
        }
        stage('update') {
            when {
                    equals expected: 'update', actual: env.ACTION
            }
            steps{
                sh """
                # Automation for Running the CF Script from Jenkins or local
                CREDS=\$(aws sts assume-role --role-arn arn:aws:iam::123456789000:role/devops- --role-session-name my-sls-session --out json)
                export AWS_ACCESS_KEY_ID=\$(echo \$CREDS | jq -r '.Credentials.AccessKeyId')
                export AWS_SECRET_ACCESS_KEY=\$(echo \$CREDS | jq -r '.Credentials.SecretAccessKey')
                export AWS_SESSION_TOKEN=\$(echo \$CREDS | jq -r '.Credentials.SessionToken')
                
                cd applicaitonlb-cloudformation

                aws cloudformation validate-template --region us-east-1 --template-body file://applicaitonlb.json

                aws cloudformation update-stack --stack-name applicaitonlb-cloudformation --region us-east-1 --template-body file://applicaitonlb.json --parameters file://parameters.json  --capabilities CAPABILITY_NAMED_IAM
                """
               }
        }
         stage('delete') {
             when {
                     equals expected: 'delete', actual: env.ACTION
             }
            steps{
                sh """
                # Automation for Running the CF Script from Jenkins or local
                CREDS=\$(aws sts assume-role --role-arn arn:aws:iam::123456789000:role/devops-role --role-session-name my-sls-session --out json)
                export AWS_ACCESS_KEY_ID=\$(echo \$CREDS | jq -r '.Credentials.AccessKeyId')
                export AWS_SECRET_ACCESS_KEY=\$(echo \$CREDS | jq -r '.Credentials.SecretAccessKey')
                export AWS_SESSION_TOKEN=\$(echo \$CREDS | jq -r '.Credentials.SessionToken')
                cd account-security
                 cd Contract-modelling

                aws cloudformation validate-template --region us-east-1 --template-body file://applicaitonlb.json

                aws cloudformation delete-stack --stack-name applicaitonlb-cloudformation --region us-east-1    
                 """
                }

        }
    }
}

