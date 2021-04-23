pipeline{
    
    agent any
    
    
    environment{
    
        REPOSITORY = "https://github.com/DC-Sena/jugg-connection.git"
        ROOT = "/root/.jenkins/workspace"
        MOUDEL_CONNECTION = "jugg-web-connection"
        DEPLOYMENT_APP_JUGG_CONNECTION="jugg-web-connection-deployment"
        
        // dev pro
        ENVIRONMENT = "dev"
        
        //9.42.426 : dev,  9.48.24 : pro
        HARBOR_IP = "9.42.426"
        
        // apply:第一次发布  update: 更新
        OPERATE = "apply"
        
        //application.properties 文件地址
        APPLICATION_PROPERTIES_FILE_PATH = "/juggconfig/application.properties"
        LOCKBACK_PROPERTIES_FILE_PATH= "/juggconfig/logback.properties"
        
        POM_PATH= "/root/.jenkins/workspace/jugg-web-connection/pom.xml"
    }
    
    stages{
        
        stage('git pull'){
            steps{
                echo "*********************START pull jugg connection moudle form github--测试${GIT_REPOSITORY} *********************"
                echo "start fetch code from git:${REPOSITORY}"
                deleteDir()
                //git credentialsId: 'jugg-web-connection', url:"${REPOSITORY}"
                
                echo "*********************copy application.properties file *********************"
                //sh "cp ${APPLICATION_PROPERTIES_FILE_PATH}  /root/.jenkins/workspace/jugg-web-connection/src/main/resources/application.properties -f"
                echo "*********************copy logback.properties file *********************"
                //sh "cp ${LOCKBACK_PROPERTIES_FILE_PATH}  /root/.jenkins/workspace/jugg-web-connection/src/main/resources/logback.properties -f"
            }
        }
        
        stage('mvn 构建+依赖'){
            steps{
                echo "*********************START maven build java project*********************"
                echo "start mvn install build..${MOUDEL_CONNECTION}"
                //sh "mvn install:install-file -DgroupId=com.ibm.db2 -DartifactId=db2jcc -Dversion=10.1 -Dpackaging=jar -Dfile=${ROOT}/${MOUDEL_CONNECTION}/cicd/lib/db2jcc-10.1.jar"
                //sh "mvn clean package -Dmaven.test.skip=true"
            }
        }
        
        
        stage('静态检查') {
            steps {
                echo "starting codeAnalyze with SonarQube......"
                //sh "mvn -f pom.xml clean compile sonar:sonar -Dsonar.host.url=http://9.1.226:9000 -Dsonar.login=15035aacaf8f99e50de0f7d667a01faa685440e5"
            }
        }
        
       
        stage('Junit') {
            steps {
              echo "starting unitTest......"
              echo "注入jacoco插件配置,clean test执行单元测试代码. jiang结果上传到将SonarQaue."        
        
        stage('Last'){
            steps{
                echo "********************* ALL END*********************"
            }
        }
        
        
    }
       
    
   post {
        always {
            echo 'One way or another, I have finished'
            /*deleteDir()*/ /* clean up our workspace */
        }
        success {
            echo 'I succeeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
    
}
