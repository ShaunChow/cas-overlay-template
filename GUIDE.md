# Generate KeyStore

keytool -genkey -alias cas.shaun.com -keyalg RSA -keysize 2048 -keypass 037988 -storepass 037988 -keystore "D:\Program Files\apache-tomcat-9.0.14-windows-x64\apache-tomcat-9.0.14\conf\cas.shaun.com.keystore" -dname "CN=cas.shaun.com,OU=shaun.com,O=shaun,L=shanghai,ST=shanghai,C=CN"

keytool -export -file "D:\Program Files\apache-tomcat-9.0.14-windows-x64\apache-tomcat-9.0.14\conf\cas.shaun.com.crt" -alias cas.shaun.com -keystore "D:\Program Files\apache-tomcat-9.0.14-windows-x64\apache-tomcat-9.0.14\conf\cas.shaun.com.keystore"

keytool -import -keystore "C:\Program Files\Java\jdk1.8.0_181\jre\lib\security\cacerts" -file "D:\Program Files\apache-tomcat-9.0.14-windows-x64\apache-tomcat-9.0.14\conf\cas.shaun.com.crt" -alias cas.shaun.com

# Change Host

C:\Windows\System32\drivers\etc\hosts

127.0.0.1 cas.shaun.com

# Change Tomcat config for https

D:\Program Files\apache-tomcat-9.0.14-windows-x64\apache-tomcat-9.0.14\conf\server.xml

    <!--
    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
    -->

    <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true">
        <SSLHostConfig>
            <Certificate certificateKeystoreFile="conf/cas.shaun.com.keystore"
                         type="RSA" 
                         certificateKeystoreType="JKS" 
                         certificateKeystorePassword="037988"/>
        </SSLHostConfig>
    </Connector>

#