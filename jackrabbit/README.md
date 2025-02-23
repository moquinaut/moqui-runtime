# Apache Jackrabbit Integration `runtime/jackrabbit`

## Setup 

Follow the steps below to run Apache Jackrabbit with Moqui.

1. Download the Jackrabbit standalone jar from http://jackrabbit.apache.org/jcr/downloads.html

2. Put the downloaded jar file here in the `runtime/jackrabbit` directory.

3. Set the Jackrabbit standalone jar file name in `runtime/classes/jackrabbit_moqui.properties`:  
   `moqui.jackrabbit_jar = jackrabbit-standalone-2.11.3.jar`

4. Enable the Jackrabbit Tool Factory (disabled by default) in `framework/src/main/resources/MoquiDefaultConf.xml`:  
   `<tool-factory class="org.moqui.impl.tools.JackrabbitRunToolFactory" init-priority="40" disabled="true"/>`

5. Add the `org.apache.jackrabbit:jackrabbit-jcr-rmi` to the classpath by uncommenting these lines in 
   `framework/build.gradle` or including them elsewhere:  
   `compile 'org.apache.jackrabbit:jackrabbit-jcr-rmi:2.12.1' // Apache 2.0`  
   `compile 'org.apache.jackrabbit:jackrabbit-jcr2dav:2.12.1' // Apache 2.0`

6. Define the Jackrabbit repositories in `framework/src/main/resources/MoquiDefaultConf.xml` (none defined by default):  
````
<repository name="main" workspace="default" username="admin" password="admin">   
    <init-param name="org.apache.jackrabbit.repository.uri" value="http://localhost:8081/rmi"/>  
</repository>
````
````  
<repository name="main" workspace="default" username="admin" password="admin">  
    <init-param name="org.apache.jackrabbit.spi2davex.uri" value="http://localhost:8081/server"/>
</repository>
````

## Optional configuration 

All content is stored in the database by default, you can update `moqui.security.UserGroupPreference` to use JCR as 
default. Check `runtime/component/mantle-usl/data/MantleInstallData.xml` for more details.  

``
<moqui.security.UserGroupPreference userGroupId="ALL_USERS" preferenceKey="mantle.content.root"
            preferenceValue="dbresource://mantle/content"/>
``  
``
<moqui.security.UserGroupPreference userGroupId="ALL_USERS" preferenceKey="mantle.content.large.root"
            preferenceValue="dbresource://mantle/content"/>
``

You can change the `preferenceValue` to `content://main/`.
