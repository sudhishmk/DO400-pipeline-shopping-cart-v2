pipeline{
    agent any
    parameters{
        booleanParam(name:"RUN_INTEGRATION_TESTS", defaultValue:true)
    }
    stages{
        stage('Test'){
            parallel{
                stage('Unit Test'){
                    steps{
                        sh './mvnw test -D testGroups=unit'
                    }
                }
                stage('Integration Test'){
                    when{
                        expression{return params.RUN_INTEGRATION_TESTS}
                    }
                    steps{
                        sh './mvnw test -D testGroups=integration'
                    }
                }
            }
        }
        stage('Build'){
            steps{
                script{
                    try{
                        sh './mvnw package -D skipTests' 
                    }
                    catch(ex){
                        echo "Error while generating JAR file"
                    }
                }
                 
            }
        }
    }
}