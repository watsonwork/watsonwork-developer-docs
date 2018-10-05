pipeline {
    agent { node { label 'standard' } }
    parameters {
        string(name: 'TIMESTAMP', defaultValue: '')
        string(name: 'PROJECT_URL', defaultValue: '')
        string(name: 'REGISTRY_TYPE', defaultValue: 'prod')
        string(name: 'GITHUB_PR_NUMBER', defaultValue: '')
        booleanParam(name: 'NPM_BUILD', defaultValue: true)
    }
    stages {
        stage('NPM Publish') {
            steps {
                script {
                    def startedAt = new Date()
                    def time = startedAt.format('yyyyMMdd-HHmmss') 
                    def path = sh(script: "pwd", returnStdout: true).trim()
                    
                    def timestamp = string(name: 'TIMESTAMP', value: time)
                    def flowWorkspace = string(name: 'WORKSPACE', value: path)
                    def flowNode = [$class: 'NodeParameterValue', name: '
                                NODE_NAME',
                                labels: [env.NODE_NAME],
                                nodeEligibility: [$class: 'AllNodeEligibility']]
                    def pipelineBuildNumber = string(name: 'PIPELINE_BUILD_NUMBER', value: env.BUILD_NUMBER)
                    def recursive = booleanParam(name: 'RECURSIVE', value: false)
                    
                    print timestamp
                    print flowWorkspace
                    print recursive
                }
            }
        }
    }
}
                    
