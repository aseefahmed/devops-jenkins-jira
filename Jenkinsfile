//START-OF-SCRIPT
node {
    def JIRA_SITE_NAME = 'jira'
    def JIRA_PROJ_NAME = 'API'
    
    def GRADLE_HOME = tool name: 'gradle-4.10.2', type: 'hudson.plugins.gradle.GradleInstallation'
    def REPO_URL = 'https://github.com/cloudacademy/devops-webapp.git'
    def DOCKERHUB_REPO = 'cloudacademydevops/webapp'

    stage('Clone') {        
        git url: REPO_URL
    }

    stage('Build') {
        // sh "${GRADLE_HOME}/bin/gradle build --info 2>&1 | tee gradle.build.${BUILD_NUMBER}.log"
        // sh "ls -la build/libs/*.war"
        git url: REPO_URL 
    }

    stage('Raise JiraIssue') {
        def issue = [fields: [ project: [key: JIRA_PROJ_NAME],
                       summary: 'Testing JIRA Created from Jenkins.',
                       description: 'New JIRA Created from Jenkins.',
                       customfield_10124: 'CRQ000000024223 is raised',
                       customfield_10143: 'FB-2209',
                       components: [[name: 'API Team']],
                       issuetype: [name: 'Story']]]
        
        def newIssue = jiraNewIssue issue: issue, site: JIRA_SITE_NAME
        
        def newIssueId = newIssue.data.key
        echo newIssueId
        
        def attachment1 = jiraUploadAttachment site: JIRA_SITE_NAME, idOrKey: newIssueId, file: "gradle.build.${BUILD_NUMBER}.log"
    }
}
//END-OF-SCRIPT
