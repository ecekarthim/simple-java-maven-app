pipeline {
    agent any

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
        rtMavenRun (
                pom: 'pom.xml',
                goals: 'clean install',
                resolverId: 'resolver-unique-id',
                deployerId: 'deployer-unique-id'
        )

        // This works
        rtPublishBuildInfo (
            serverId: 'Devops-Jfrog'
        )
}
