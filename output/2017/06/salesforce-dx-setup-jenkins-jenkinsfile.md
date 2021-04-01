---
layout: "post.11ty.js"
title: "Salesforce DX - Setup Jenkins - Jenkinsfile"
date: "2017-06-21"
tags: 
  - "Blog"
  - "Jenkins"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "salesforce-dx-setup-jenkins-jenkinsfile"
coverImage: "sfdx-10-header.png"
---

In [Salesforce DX – Setup Jenkins](https://wipdeveloper.wpcomstaging.com/2017/06/19/salesforce-dx-setup-jenkins/) we set up Jenkins to pull from our Github repository.  It really didn't do anything else since there was no `Jenkinsfile` to explain to Jenkins what to do.  Lets provide a remedy for that now.  But first...

## Jenkinsfile... wha?

When Jenkins 2.0 was released they introduced this concept of "[Pipeline as Code](https://wiki.jenkins-ci.org/display/JENKINS/2.0+Pipeline+as+Code)".  It was a new way to configure a build pipeline for Jenkins.  All described in a human-editable file called a `Jenkinsfile`.   The `Jenkinsfile` was defined in the repository that was to be built.  Since we used the default setup it was looking for a file at the root called `Jenkinsfile` and since we didn't add one yet, **SURPRISE!** Nothing happened.

If you used Jenkins before version 2.0 was release build setup were configured manually.  If you had changes the only way to track them was if the user made notes.  Should people make notes when updating configurations?  Yes!  Do they?  Not always.   Pipeline as Code means all changes are now tracked by the same source control that tracks  code changes.

All that to say, We need a `Jenkinsfile`.

## Jenkinsfile Setup

In our project let's add a new file named `Jenkinsfile` at the root.  for our starter `Jenkinsfile` we are going to copy the one from [forcedotcom](https://github.com/forcedotcom)/[sfdx-dreamhouse](https://github.com/forcedotcom/sfdx-dreamhouse) and then adjust it to suit our needs to let's go get the contents of it and add it to our file.   Now let's look at what we have.

#### Import `JsonSlurperClassic`

#!groovy
import groovy.json.JsonSlurperClassic

For lines `1` and `2` we import `JsonSlurperClassic` so we can use it to parse json responses later on.

#### Open `node`

node {

#### Close `node`

}

At Line `3` we open a `node` statement that we close on line `64`.  What the `node` statement does is create the work space and allocate the executor for the build to occur.   If we didn't do this we couldn't build anything.

#### Define Variables

def BUILD\_NUMBER=env.BUILD\_NUMBER
def RUN\_ARTIFACT\_DIR="tests/${BUILD\_NUMBER}"
def SFDC\_USERNAME

def HUB\_ORG=env.HUB\_ORG\_DH
def SFDC\_HOST = env.SFDC\_HOST\_DH
def JWT\_KEY\_CRED\_ID = env.JWT\_CRED\_ID\_DH
def CONNECTED\_APP\_CONSUMER\_KEY=env.CONNECTED\_APP\_CONSUMER\_KEY\_DH

def toolbelt = tool 'toolbelt'

For lines `5` through `14` we define some variables to use later on.  Most of the values are set from the environment.  Line `14` we define the `toolbelt` this is the SFDX CLI .  Since we haven't set up any of these environment variables or the access to the SFDX CLI we will have to circle back to Jenkins ot set these up next time.

#### Checkout Source

stage('checkout source') {
    // when running in multi-branch job, one must issue this command
    checkout scm
}

Line `16` we have a `stage` directive named "checkout source\`.  During this stage we will get the code for the build.  Using the `checkout` keyword will checkout the code from the source control specified in the Jenkins setup.  The `scm` variable is that tells the `checkout` command what reversion triggered the build.

#### Open`withCredentials`

withCredentials(\[file(credentialsId: JWT\_KEY\_CRED\_ID, variable: 'jwt\_key\_file')\]) {

#### Close `withCredentials`

}

At line `21` we open a `withCredentials` snippet.  This is provided by the [Credentials Binding Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Credentials+Binding+Plugin).  The credentials we use are provided by a combination of the variable we defined earlier and the secret file we saved [last time](https://wipdeveloper.wpcomstaging.com/2017/06/19/salesforce-dx-setup-jenkins/).  This will prevent any of our "secrets" from showing up in the building log.

#### Create Scratch Org

stage('Create Scratch Org') {

    rc = sh returnStatus: true, script: "${toolbelt}/sfdx force:auth:jwt:grant --clientid ${CONNECTED\_APP\_CONSUMER\_KEY} --username ${HUB\_ORG} --jwtkeyfile ${jwt\_key\_file} --setdefaultdevhubusername --instanceurl ${SFDC\_HOST}"
    if (rc != 0) { error 'hub org authorization failed' }

    // need to pull out assigned username
    rmsg = sh returnStdout: true, script: "${toolbelt}/sfdx force:org:create --definitionfile config/workspace-scratch-def.json --json --setdefaultusername"
    printf rmsg
    def jsonSlurper = new JsonSlurperClassic()
    def robj = jsonSlurper.parseText(rmsg)
    if (robj.status != "ok") { error 'org creation failed: ' + robj.message }
    SFDC\_USERNAME=robj.username
    robj = null

}

Here we are creating a scratch org.  At line `24` we run a shell command and get the return status of it.  As long as the return status is `0` everything is ok.  Line `28` we use a second shell command to call the same `sfdx force:org:create` that we have used in the past but with the added parameter of `--json`.  The `--json` parameter tells `sfdx` to format the results as json.  Those results are parse on line `31` with an instance of the `JsonSlurperClassic` we imported all the way back on line `2`.  As long as the `robj.status` is ok on line `32` we save teh username that was returns in the variable that was defined on line `7` before nulling the `robj` out.

#### Push to Test Org

stage('Push To Test Org') {
    rc = sh returnStatus: true, script: "${toolbelt}/sfdx force:source:push --targetusername ${SFDC\_USERNAME}"
    if (rc != 0) {
        error 'push failed'
    }
    // assign permset
    // rc = sh returnStatus: true, script: "${toolbelt}/sfdx force:user:permset:assign --targetusername ${SFDC\_USERNAME} --permsetname WIPDeveloper"
    // if (rc != 0) {
    //     error 'permset:assign failed'
    // }
}

With the `Push to Test Org` stage we push the source to the scratch org we just created by specifying the `--targetusername` as what was saved on line `33`.  Provided there are no errors we assign a permission set to the user that was created at line `33`.

> I don't have any permission sets in my sample code yet so I have this commented out.

#### Run Tests

stage('Run Apex Test') {
    sh "mkdir -p ${RUN\_ARTIFACT\_DIR}"
    timeout(time: 120, unit: 'SECONDS') {
        rc = sh returnStatus: true, script: "${toolbelt}/sfdx force:apex:test:run --testlevel RunLocalTests --outputdir ${RUN\_ARTIFACT\_DIR} --resultformat tap --targetusername ${SFDC\_USERNAME}"
        if (rc != 0) {
            error 'apex test run failed'
        }
    }
}

This may surprise you but with the `Run Apex Test` stage we will run the Apex Tests.  _Surprise!_ More seriously though at line `51` we create a directory with the `RUN_ARTIFACT_DIR` that was defined and assigned at line `6`.  At line `52` we use the `timeout` option to specify a timeout period of 120 seconds.  If it takes longer then the time specified Jenkins will abort the Pipeline.

#### Collect Results

stage('collect results') {
    junit keepLongStdio: true, testResults: 'tests/\*\*/\*-junit.xml'
}

With the `Collect Results` stage we use the junit plugin to collect the results.

## Commit, Push and Nothing

With our Jenkins file defined let's commit it to the repository and push it to the origin.  Don't get too excited though as we haven't set up those environment variables yet so your Jenkins may detect the change it will not build successfully yet.

## Conclusion

We are almost ready for a successful build, one might way we are so close yet so `var` away.  Get it?  Let me know by leaving a comment below, emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com) or following and yelling at me on [Twitter/BrettMN](https://twitter.com/BrettMN).
