pipeline {
    agent any
    stages {
        stage('calculate diffs') {
            steps {

                // get the latest release 
                sh 'git describe --tags `git rev-list --tags --max-count=1`'
                echo "calculate diffs"
            }
        }
        stage('manifest creation') {
            steps {
                echo "manifest creation"
            }
        }    
        stage('Validate CF Templates') {
            steps {
                script {
                    def templatesDir = ''  // assuming this is where the repo is cloned test addsss

                    // List all CloudFormation template files in the directory
                    def templateFiles = findFiles(glob: '**/*.json')

                    //Loop through each template file and validate
                    for (def templateFile in templateFiles) {
                       def templatePath = templateFile.path
                       echo "Validating template: ${templatePath}"

                    //  Execute the AWS CLI command to validate the template
                       sh "aws cloudformation validate-template --template-body file://${templatePath}"
                    }
                }
            }
        }
        stage('Lint CF Templates') {         
            steps {
                // Run your build and test commands here
                echo "cfn-nag the templates"
            }
        }        
        stage('push to artifactory') {         
            steps {
                // Run your build and test commands here
                echo "push to artifactory"
            }
        }
        stage('push to staging bucket') {
            steps {
                echo "push to staging bucket"
            }
        }        
    }
}
