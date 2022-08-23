// This is the template file for BPA Jenkins jobs.
// Do not modify this file without consulting bpa-engg-leads <bpa-engg-leads@cisco.com>
// For running Jenkins job against your private branch,
// you may modify this file in your branch, and make sure
// to .gitignore it
// For instructions on setting up a Jenkins job,
// Refer to the ReadMe <TBD>
        def value = 'version_increment'
        withEnv(['BPA_BRANCH=BPA_DEVELOP_3.2.2', 'PACKAGING_REPO=develop']){
        stage('Preparation') {
            sh 'uname -a'
            deleteDir()

            

            checkout(
                    [
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
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
                                credentialsId: '685f9bfc-289e-4228-8aa6-c00888ca3136',
                                url: 'https://github.com/dhanvanthari/yamlrepo.git'
                            ]
                        ]
                    ]
                )
			
            checkout(
                    [
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
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
                                credentialsId: '685f9bfc-289e-4228-8aa6-c00888ca3136',
                                url: 'https://github.com/dhanvanthari/yamlrepo.git'
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
                                    description: 'Select the bundle', 
                                    filterLength: 1, 
                                    filterable: false, 
                                    name: 'Build', 
                                    script: [
                                        $class: 'GroovyScript', 
                                        fallbackScript: [
                                            classpath: [], 
                                            sandbox: true, 
                                            script: 
                                                "return['Could not get the bundles']"
                                        ], 
                                        script: [
                                            classpath: [], 
                                            sandbox: true, 
                                            script: 
                                                "return['Build all core packages:selected','Build all Addon packages','Build both core and Addon packages']"
                                        ]
                                    ]
                                ]
							])
 						])
                    }
                }
           				
		    }						
        
       
        }
