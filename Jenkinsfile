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

node {
    propsFile = readFile("build.properties")
    props.load(new StringReader(propsFile))
    designerDockerImageNo = props.get("docker_image_designer")
    buildUtilsBuildNo = props.get("BuildUtils_ArtifactNO")
    testUtilsBuildNo = props.getProperty("TestUtils_ArtifactNO")
    validateBranchName = props.getProperty("validate_BranchName")
    volbaseBranchName = props.getProperty("volbase_BranchName")
}

pipeline {
    agent any
    environment{
            DEPLOY_TO="$volbaseBranchName"
        }
    stages {
        stage('build the code') {
            steps {
                when {
                      environment name: 'DEPLOY_TO', value: 'master'
                      }
                echo "integration is successful"
		        build job: 'scan',
                        parameters: [
                                booleanParam(name: 'MOUNT_MAVEN', value: true),
                                string(name: 'BUILD_BRANCH', value: 'master'),
                                string(name: 'USER_BUILD_TAG', value: 'N/A'),
                                 string(name: 'UPSTREAM_BUILD_BRANCH', value: 'develop')
                        ]
            }
        }
    }
}