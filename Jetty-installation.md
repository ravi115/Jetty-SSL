
## Jetty Installation.

[latest jetty can be installed from here.](https://www.eclipse.org/jetty/download.html)

- Once the jetty file is downloaded based on the platform, then extract the jetty.
- go to the jetty folder, there will be **start.jar** needs to run and jetty will start running.

**Install jetty on linux/ubuntu as deamon as serverice**

- Go to the /opt directory.
  
      cd /opt
    
- To download the jetty using below link: 

      sudo wget -c http://repo1.maven.org/maven2/org/eclipse/jetty/jetty-distribution/9.3.12.v20160915/jetty-distribution-9.3.12.v20160915.tar.gz
 
- Rename the jetty after extracting it.

      sudo tar -xvf jetty-distribution-9.3.12.v20160915.tar.gz
      
      sudo mv jetty-distribution-9.3.12.v20160915.tar.gz jetty
 
- Create a user called Jetty and configure the correct file ownership:

      sudo useradd -m jetty
      
      sudo chown -R jetty:jetty /opt/jetty/
      
- Symlink the jetty.sh script to the /etc/init.d/ directory to create a start up script file:

      sudo ln -sf /opt/jetty/bin/jetty.sh /etc/init.d/jetty9
      
- Now, you need to create a configuration file for Jetty. Open a file:

      sudo /etc/default/jetty9
  add below configuration: 
   
      JETTY_HOME=/opt/jetty
      JETTY_USER=jetty
      JETTY_PORT=8080
      JETTY_HOST=your_server_IP
      JETTY_LOGS=/opt/jetty/logs/
      
- Navigate to the Jetty installation directory:
  
       cd /opt/jetty
       
- Next, delete the webapps directory since there is nothing in it and copy the webapps directory from demo-base. It is a test and demo data from Jetty.

      sudo  rm -rf webapps/

      sudo cp -r demo-base/webapps/ /opt/jetty/
      
- To start the jetty: 

      service jetty start
   
