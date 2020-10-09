node {
    def VELOCITY_TENANT_ID="5ade13625558f2c6688d15ce"
    
    //VELOCITY_APP_NAME must match your Velocity pipeline application name
    def VELOCITY_APP_NAME="cheng1-ucv-ocptest-02"
    
    //Do not change below this line.
    def GIT_COMMIT
        
    stage ('Git') {
		checkout scm
		GIT_COMMIT = sh(script: 'git rev-parse HEAD', returnStdout: true).trim()		
		
		echo "Stage-git: GIT_COMMIT=${GIT_COMMIT}"
		echo "WORKSPACE: ${WORKSPACE}"	
		sh """
		   pwd
		   ls -lat		   
	    """
    }
    
    stage ('Set Properties') {
         currentBuild.displayName = "1.1.1.${BUILD_NUMBER}"
         //currentBuild.displayName = "${buildNumber}"
         snapshotName    = "${currentBuild.displayName}"	
    }
  		          	
	stage ("Build") {
        echo "Building ${VELOCITY_APP_NAME} (versionName:${currentBuild.displayName}, GIT_COMMIT:${GIT_COMMIT})"	    
 	    echo "VELOCITY_TENANT_ID: ${VELOCITY_TENANT_ID}"
        echo "revision: ${GIT_COMMIT}"
        echo "appName: ${VELOCITY_APP_NAME}"
        echo "versionName: ${currentBuild.displayName}"
        step($class: 'UploadBuild', 
           tenantId: "${VELOCITY_TENANT_ID}",
           revision: "${GIT_COMMIT}",
           appName: "${VELOCITY_APP_NAME}",
           versionName:"${currentBuild.displayName}",
           requestor: "admin", id: "${currentBuild.displayName}"
        )
    }
    
}
