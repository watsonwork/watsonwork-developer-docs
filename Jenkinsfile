/**
 * checkout source code from a repo that isn't this project repo
 * needed to check out npm build tools for toscana projects
 * @param repo the repository to check out
 * @param dir subdirectory to check the source code out to
 * @param ctx the build context
 * @param path the path for a sparsecheckoutpath, default is .
*/
def checkoutRepo(repo, directory, path){
    def extensions = [[$class: 'SparseCheckoutPaths', sparseCheckoutPaths: [[$class:'SparseCheckoutPath', path: path]]]]
    if(!path){
        extensions = []
    }
    dir(directory){
      checkout changelog: false, poll: false,
          scm: [$class: 'GitSCM',
                branches: [[name: "master"]],
                doGenerateSubmoduleConfigurations: false,
                extensions: extensions,
                submoduleCfg: [],
                userRemoteConfigs: [[credentialsId: '4c9bec59-7c0e-4d28-a875-395622cc4475',
                                     name: "origin",
                                     url: repo]]
                ]
    }
}

pipeline {
    agent { node { label 'standard' } }
    stages {
        stage('NPM Publish') {
            steps {
                script {
                    try {
                        checkoutRepo("https://github.ibm.com/toscana/pipeline-tools/", ".jenkins/build-tools", "npm/")

                        def startedAt = new Date()
                        def time = startedAt.format('yyyyMMdd-HHmmss')
                        currentBuild.displayName = time
                        def path = sh(script: "pwd", returnStdout: true).trim()

                        def timestamp = string(name: 'TIMESTAMP', value: time)
                        def flowWorkspace = string(name: 'WORKSPACE', value: path)
                        def flowNode = [$class: 'NodeParameterValue', name: 'NODE_NAME',
                                    labels: [env.NODE_NAME],
                                    nodeEligibility: [$class: 'AllNodeEligibility']]
                        def pipelineBuildNumber = string(name: 'PIPELINE_BUILD_NUMBER', value: env.BUILD_NUMBER)
                        def recursive = booleanParam(name: 'RECURSIVE', value: false)

                        build(job: 'NPM/Publish', parameters: [timestamp, flowWorkspace, flowNode, pipelineBuildNumber, recursive])
                    } finally {
                        sh "rm -rf ./*"
                    }
                }
            }
        }
    }
}
