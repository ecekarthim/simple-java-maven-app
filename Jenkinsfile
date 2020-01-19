pipeline {
    agent any
    stages {
            stage('artifcats') {
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
        rtMavenRun (
                pom: 'pom.xml',
                goals: 'help:effective-settings',
                //goals: 'deploy',
                resolverId: 'resolver-unique-id',
                deployerId: 'deployer-unique-id'
        )

        // This works
        rtPublishBuildInfo (
            serverId: 'Devops-Jfrog'
        )

          }
    }

        stage ('Publish build info') {
            steps {
                archiveArtifacts 'target/*.jar'
                rtPublishBuildInfo (
                    serverId: "Devops-Jfrog"
                )
            }
        }

}
}
