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
        stage ('upload') {
            steps {
                rtUpload (
                    serverId: "Devops-Jfrog",
                    spec: '''{
                          "files": [
                            {
                              "pattern": "target/**.jar",
                              "target": "libs-snapshot-local"
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
