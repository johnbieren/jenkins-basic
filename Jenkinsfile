#!/usr/bin/env groovy

// Check out libraries
def libraries = ['ci-pipeline': ['master', 'https://github.com/CentOS-PaaS-SIG/ci-pipeline.git'],
                 'contra-lib': ['master', 'https://github.com/openshift/contra-lib.git']]

libraries.each { name, repo ->
    library identifier: "${name}@${repo[0]}",
            retriever: modernSCM([$class: 'GitSCMSource',
                                  remote: repo[1]])
}

import net.sf.json.JSONObject
import groovy.json.JsonOutput

properties(
        [
                buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '2', daysToKeepStr: '', numToKeepStr: '2')),
                parameters([
                    string(name: 'CI_MESSAGEf',
                    description: 'The fedmsg',
                    defaultValue: '{}'),
                ])
        ]
)

node('master') {
    //ciPipeline() {
        timestamps {
            try {
                deleteDir()
                stage('example-stage') {
                //ciStage('example-stage') {
                    env.topicPrefix = 'abc'
                    env.effortName = 'test'
                    env.teamName = 'test'
                    env.teamEmail = 'test'
                    env.pipelineId = 'test'
                    sendPipelineStatusMsg('running')
                    
                }
            } catch (e) {
                println("error is " + e)
                throw e
            }
        }
    //}
}

