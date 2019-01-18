node {
   stage('init') {
      checkout scm
   }
   stage('build') {
      sh '''
         
         mvn clean package
         cd target
         cp ../src/main/resources/web.config web.config
         cp ../src/main/resources/start.sh start.sh
         cp gs-spring-boot-0.1.0.jar app.jar 
         zip todo.zip app.jar web.config start.sh
      '''
   }
   stage('deploy') {
      azureWebAppPublish azureCredentialsId: env.AZURE_CRED_ID,
      resourceGroup: env.RES_GROUP, appName: env.WEB_APP, filePath: "**/todo.zip"
   }
}
