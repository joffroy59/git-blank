node {
    
    properties(
        [
            parameters([
                string(name: 'GIT_BRANCH', defaultValue: 'main', description: 'branch git', trim: true)
                ]), 
            [$class: 'RebuildSettings', autoRebuild: false, rebuildDisabled: false]
        ]
    )
    
    def mvnHome
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
        git credentialsId: 'github-joffroy59', url: 'https://github.com/joffroy59/git-blank.git', branches: params.GIT_BRANCH
        // checkout scmGit(branches: [[name: params.GIT_BRANCH]], extensions: [], userRemoteConfigs: [[credentialsId: 'github-joffroy59', url: 'https://github.com/joffroy59/git-blank.git']])
    }
    stage('Manage changelog') {
    }
    stage('Results') {
        echo "TODO"
    }
}
