pipeline {
    agent any
    stages {
    stage('Deploy') {
    environment {
        MAVEN_HOME = '/usr/share/maven'
        JAVA_HOME= '/usr/local/openjdk-8'
    }
    steps {
        rtMavenResolver (
                id: 'resolver-unique-id',
                serverId: 'Devops-Jfrog',
                releaseRepo: 'libs-release-local',
                snapshotRepo: 'libs-snapshot-local'
        )
        rtMavenDeployer (
                id: 'deployer-unique-id',
                serverId: 'Devops-Jfrog',
                releaseRepo: 'libs-release-local',
                snapshotRepo: 'libs-snapshot-local'
        )
          }
    }
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MAVEN_HOME', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "deployer-unique-id",
                    resolverId: "resolver-unique-id"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "Devops-Jfrog"
                )
            }
        }

}
}
