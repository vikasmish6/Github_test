pipeline{

    agent any
    
   parameters {
    // define input parameters
        string defaultValue: 'file1', name: 'Filename'
        string defaultValue: '1.0.0', name: 'Version'
        string defaultValue: 'Dev', name: 'Environment'
    } 
  environment {
    //define Global Environment Variables
    Intermidiate_variable = "1"
    GlobalFilename = ""
    GlobalVersion = ""
    GlobalEnvironment = ""
    }
        stages{
            //Specify list of stages in which the job is divided
            stage("Reading variables"){
                //divide single job into multiple phases
                steps{
                    // steps to be in the stage
                    script{
                        //Actual implementation code
                        GlobalFilename = params.Filename
                        GlobalEnvironment = params.Environment
                        GlobalVersion = params.Version
                    }

                }

        }
        stage("Printing variables"){

                steps{
                    script{
                        print(env.Version)
                        //print($BUILD_NUMBER)
                    }                   

                }
        }

    stage("download Maven project"){

                    steps{
                        script{
                            bat 'mkdir maven'
                            bat 'cd maven'
                            git branch: 'main', credentialsId: 'New_Github_token', url: 'https://github.com/vikasmish6/maventraining.git'
                        }                   

                    }
            }
         stage("Build Maven project"){

                steps{
                    script{
                        bat 'cd maven'
                        bat 'mvn clean install'
                    }                   

                }
        }

    }
    post {
        always {
            bat 'echo \'build completed\''
            // One or more steps need to be included within each condition's block.
        }
    }
}