Run your Apache Tomcat and Juddi with MySQL on OpenShift
========================================================
This git repository helps you get up and running quickly with Apache Tomcat 7.0.42 and Juddi 3.1.5 with MySQL installations on OpenShift.

Create a Do It Yourself (DIY) app on OpenShift
----------------------------------------------
<a href="https://openshift.redhat.com/app/account/new">Create an account</a> and install the <a href="https://www.openshift.com/developers/rhc-client-tools-install">command-line client tools</a>.

Create a DIY application:

    rhc app create tomcatjuddi diy-0.1 mysql-5.1 phpmyadmin-3.4

Configure MySQL
---------------
Go to your phpMyAdmin URL: http://tomcatjuddi-$yournamespace.rhcloud.com/phpmyadmin/

Login with your MySQL credentials. Click on SQL tab at the top to run SQL query/queries on server.

Type in the following commands; replacing $OPENSHIFT_MYSQL_DB_HOST appropriately and then click Go:

    CREATE USER 'juddi'@'$OPENSHIFT_MYSQL_DB_HOST' IDENTIFIED BY 'juddi';
    CREATE DATABASE juddi;
    GRANT ALL PRIVILEGES ON juddi.* TO 'juddi'@'$OPENSHIFT_MYSQL_DB_HOST';

Get the quickstart running
--------------------------
Grab this quickstart project and make it work for you!

    cd tomcatjuddi
    git remote add upstream -m master git://github.com/petcna/openshift-tomcat-juddi-quickstart.git
    git pull -s recursive -X theirs upstream master
    git push

That's it, you can now checkout your tomcat at: http://tomcatjuddi-$yournamespace.rhcloud.com

Your juddi is available at: http://tomcatjuddi-$yournamespace.rhcloud.com/juddiv3

Juddi user guide can be accessed from <a href="http://juddi.apache.org/docs/3.x/userguide/html/index.html">here</a>.

Tutorial on how to publish a web service to juddi can be found <a href="http://thoughtsasaservice.wordpress.com/2011/08/27/how-to-publish-a-web-service-to-juddi">here</a>.

<a href="http://www.soapui.org">SoapUI</a> can be used to deal with juddi web services.

Unfortunately, juddi portal is not available in this quickstart. It is planned to be added soon.

By placing WARs (either WAR archives or exploded WARs) in the diy/tomcat/webapps folder, those applications will be deployed and redeployed upon each <code>git push</code>. Likewise, applications (including the sample applications provided by Tomcat) can be deleted from that folder so they will no longer be deployed.

The default managing account is tomcat/openshift; this can be changed by altering the diy/tomcat/conf/tomcat-users.xml file, committing the change within your secure OpenShift Git account and issuing another <code>git push</code>.

License
-------
This code is dedicated to the public domain to the maximum extent permitted by applicable law, pursuant to CC0 <a href="http://creativecommons.org/publicdomain/zero/1.0/">http://creativecommons.org/publicdomain/zero/1.0/</a>

