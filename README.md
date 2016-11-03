HAN SSO startup:
mvn package

modify local tomcat:
1.copy  /etc/keystore to you ${tomcat_home}/confg
2. modify ${tomcat_home}/confg/server.xml add following:
	 <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true">
        <SSLHostConfig>
            <Certificate certificateKeystoreFile="conf/keystore"
                         type="RSA" />
        </SSLHostConfig>
    </Connector>
3. use https://localhost:8443/ as login point.
4. you can use casuser/Mellon login, or add some use in 
src/main/resources/cas.properties line 290,accept.authn.users property

next:
read cas.properties for db user support..

CAS Overlay Template
============================

Generic CAS maven war overlay to exercise the latest versions of CAS. This overlay could be freely used as a starting template for local CAS maven war overlays. The CAS services management overlay is available [here](https://github.com/Jasig/cas-services-management-overlay).

# Versions
```xml
<cas.version>4.2.x</cas.version>
```

# Requirements
* JDK 1.7+

# Configuration

The `etc` directory contains the configuration files that need to be copied to `/etc/cas`.

Current files are:

* `cas.properties`
* `log4j2.xml`

# Build

```bash
mvnw clean package
```

or

```bash
mvnw.bat clean package
```

# Deployment

## Embedded Jetty

* Create a Java keystore at `/etc/cas/jetty/thekeystore` with the password `changeit`.
* Import your CAS server certificate inside this keystore.

```bash
mvnw jetty:run-forked
```

CAS will be available at:

* `http://cas.server.name:8080/cas`
* `https://cas.server.name:8443/cas`

## External
Deploy resultant `target/cas.war` to a Servlet container of choice.


Authentication:
JDBC:
https://apereo.github.io/cas/4.2.x/installation/Database-Authentication.html

shiro:
https://apereo.github.io/cas/4.2.x/installation/Shiro-Authentication.html

