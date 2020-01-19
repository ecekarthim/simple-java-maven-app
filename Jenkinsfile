pipeline {
    agent any
    stages {
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MAVEN_HOME', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                )
            }
        }
        stage ('Publish to JFrog') {
            steps {
                rtUpload (
                    serverId: "Devops-Jfrog",
                    spec: '''{
                          "files": [
                            {
                              "pattern": "target/**.jar",
                              "target": "libs-snapshot-local/my_app"
                            }
                          ]
                    }'''
                    
                )
            }
        }

       
        /*stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "Devops-Jfrog"
                )
            }
        }*/

}
}
