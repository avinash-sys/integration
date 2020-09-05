properties(
        [
                buildDiscarder(
                        logRotator(artifactDaysToKeepStr: '',
                                artifactNumToKeepStr: '',
                                daysToKeepStr: '10',
                                numToKeepStr: '10'
                        )
                ),
                disableConcurrentBuilds(),
                durabilityHint('MAX_SURVIVABILITY'),
                disableResume(),
                [
                        $class      : 'CopyArtifactPermissionProperty',
                        projectNames: '*'
                ],
                parameters(
                        [
                                booleanParam(
                                        defaultValue: true,
                                        description: 'Do u want to use mounted maven?',
                                        name: 'MOUNT_MAVEN'
                                ),
                                string(
                                        defaultValue: 'N/A',
                                        description: 'To build a branch',
                                        name: 'BUILD_BRANCH',
                                        trim: true
                                ),
                                string(
                                        defaultValue: 'N/A',
                                        description: 'To build a tag',
                                        name: 'USER_BUILD_TAG',
                                        trim: true
                                )
                        ]
                )
        ]
)

pipeline {
    agent any
    stages {
        stage('build the code') {
            steps {
                echo "integration is successful"
		        build job: 'scan',
                        parameters: [
                                booleanParam(name: 'MOUNT_MAVEN', value: true),
                                string(name: 'BUILD_BRANCH', value: 'master'),
                                string(name: 'USER_BUILD_TAG', value: 'N/A'),
                        ]
            }
        }
    }
}