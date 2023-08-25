/* groovylint-disable NoDef */
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
        //git credentialsId: 'github-joffroy59', url: 'https://github.com/joffroy59/git-blank.git'
        checkout scmGit(branches: [[name: params.GIT_BRANCH]], extensions: [], userRemoteConfigs: [[credentialsId: 'github-joffroy59', url: 'https://github.com/joffroy59/git-blank.git']])
    }
    stage('Manage changelog') {
      manageChangelog()
    }
    stage('Results') {
        echo 'TODO'
    }
}

def manageChangelog() {
  def changeLogSets = currentBuild.changeSets
  for (int i = 0; i < changeLogSets.size(); i++) {
    def entries = changeLogSets[i].items
    for (int j = 0; j < entries.length; j++) {
      def entry = entries[j]
      // echo "${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}"
      println("${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}")
      def files = new ArrayList(entry.affectedFiles)
      for (int k = 0; k < files.size(); k++) {
        def file = files[k]
        // echo "  ${file.editType.name} ${file.path}"
        println("  ${file.editType.name} ${file.path}")
      }
    }
  }
}
