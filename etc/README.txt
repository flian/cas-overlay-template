1. copy keystore and localcas.cer to ${TOMCAT_HOME}/conf
2. client side, add host <CAS IP> hna.local.cas.server
3. import localcas.cer into jdk keystore,using:
    keytool -import -file  localcas.cer -keystore "%JAVA_HOME%\jre\lib\security\cacerts" -alias tomcat
    using command
    keytool -list -keystore "%JAVA_HOME%\jre\lib\security\cacerts" | findstr /i tomcat
    issue key imported in jdk.
4. config your client point cas server "hna.local.cas.server"