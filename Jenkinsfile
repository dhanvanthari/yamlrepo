// This is the template file for BPA Jenkins jobs.
// Do not modify this file without consulting bpa-engg-leads <bpa-engg-leads@cisco.com>
// For running Jenkins job against your private branch,
// you may modify this file in your branch, and make sure
// to .gitignore it
// For instructions on setting up a Jenkins job,
// Refer to the ReadMe <TBD>
node('apjc-sio-slv02') {
        def value = 'version_increment'
        withEnv(['BPA_BRANCH=BPA_DEVELOP_3.2.2', 'PACKAGING_REPO=develop']){
        stage('Preparation') {
            sh 'uname -a'
            deleteDir()

            

            checkout(
                    [
                        $class: 'GitSCM',
                        branches: [[name: '*/UC-12']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [
                            [
                                $class: 'RelativeTargetDirectory',
                                relativeTargetDir: 'bpa-ci-cd'
                            ],
                            [
                                $class: 'CloneOption',
                                noTags: false,
                                reference: '',
                                shallow: true,
                                timeout: 30
                            ]
                        ],
                        submoduleCfg: [],
                        userRemoteConfigs: [
                            [
                                credentialsId: 'bpabuilduser.gen',
                                url: 'https://bitbucket-eng-sjc1.cisco.com/bitbucket/scm/cf-bpa/bpa-ci-cd.git'
                            ]
                        ]
                    ]
                )
			
            checkout(
                    [
                        $class: 'GitSCM',
                        branches: [[name: '*/UC-12']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [
                            [
                                $class: 'RelativeTargetDirectory',
                                relativeTargetDir: 'bpa-ci-cd-non-core'
                            ],
                            [
                                $class: 'CloneOption',
                                noTags: false,
                                reference: '',
                                shallow: true,
                                timeout: 30
                            ]
                        ],
                        submoduleCfg: [],
                        userRemoteConfigs: [
                            [
                                credentialsId: 'bpabuilduser.gen',
                                url: 'https://bitbucket-eng-sjc1.cisco.com/bitbucket/scm/cf-bpa/bpa-ci-cd-non-core.git'
                            ]
                        ]
                    ]
                )			

        }
		stage('Parameters'){
                steps {
                    script {
                    properties([
                            parameters([
                                [$class: 'ChoiceParameter', 
                                    choiceType: 'PT_RADIOs', 
                                    description: 'Select the Environemnt from the Dropdown List', 
                                    filterLength: 1, 
                                    filterable: false, 
                                    name: 'Env', 
                                    script: [
                                        $class: 'GroovyScript', 
                                        fallbackScript: [
                                            classpath: [], 
                                            sandbox: false, 
                                            script: 
                                                "return['Could not get The environemnts']"
                                        ], 
                                        script: [
                                            classpath: [], 
                                            sandbox: false, 
                                            script: 
                                                "return['dev','stage','prod']"
                                        ]
                                    ]
                                ]
							])
 						])
                    }
                }
           				
		    }						
        
       
        }
}
