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
      manageReportChangelog()
    }
    stage('Results') {
        echo 'TODO'
    }
}

def manageChangelog() {
  def changeLogSetsNew = currentBuild.changeSets
  def changeLogToReturn=""
  println(changeLogSetsNew)
  println("changelog size:" + changeLogSetsNew.size())
  changeLogSetsNew
      .each { changeLogSet ->
          println(changeLogSet)
          changeLogSet.items.each { changeSet ->
              def commmitDate = new Date().format("EEE MMM dd yy HH:mm:ss", TimeZone.getTimeZone('GMT+5:30'))
              changeLogToReturn += "<${changeLogSet.browser.repoUrl}\n/commit/${changeSet.commitId}|${changeSet.msg}> by ${changeSet.author} on ${commmitDate}, commit details below\n"
              changeSet.affectedFiles.each { file ->
                  changeLogToReturn += "\t\t${file.editType.name.capitalize()} - ${file.path}\n"
              }
          }
      }
  println(changeLogToReturn)
}

def manageReportChangelog() {
  def changeLogSetsNew = currentBuild.changeSets
  def changeLogToReturn=""
  println(changeLogSetsNew)
  println("changelog size:" + changeLogSetsNew.size())
  changeLogSetsNew
      .each { changeLogSet ->
          def browser = changeLogSet.browser
          println("changeLogSet ${changeLogSet}")
/*           println("browser.getChangeSetLink(changeLogSet) ${browser.getChangeSetLink(changeLogSet)}")
 */
          changeLogSet.items.each { changeSet ->
              def commmitDate = new Date().format("EEE MMM dd yy HH:mm:ss", TimeZone.getTimeZone('GMT+2:00'))
              println("changeSet ${changeSet}")
              println("browser.getChangeSetLink(changeSet) ${browser.getChangeSetLink(changeSet)}")
              println("browser.repoUrl ${browser.repoUrl}")
              changeLogToReturn += "<${changeLogSet.browser.repoUrl}\n/commit/${changeSet.commitId}|${changeSet.msg}> by ${changeSet.author} on ${commmitDate}, commit details below\n"
              changeSet.affectedFiles.each { file ->
                  changeLogToReturn += "\t\t${file.editType.name.capitalize()} - ${file.path}\n"
              }
          }
      }
  println(changeLogToReturn)
}
