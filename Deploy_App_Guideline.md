#How To: Deploy an App on Predix
Written by: Brandon Goldman (ITLP Intern)
----

####Objective:
This tutorial is meant to show you how to set up the Predix Devbox toolset and get your first app up and running on Predix.

####What you need:
1. Predix Account (https://www.predix.io)
2. Predix DevBox (https://www.predix.io/services/other-resources/devbox.html)
3. VMWare Workstation Player (http://www.vmware.com/products/player/)
4. Github Account (https://www.github.com/join)

It is also recommended you have a basic understanding of how a Linux terminal works, including how to move around directories and debug errors. Here is a tutorial I recommend: http://ryanstutorials.net/linuxtutorial/

----

####Set Up Predix Devbox
1. Once you have your Predix account set up, download Devbox and place the unzipped file on your desktop.
2. Download VMWare Workstation Player.
3. Inside VMWare, click "Create a New Virtual Machine".
4. Click "Installer disc image file (iso):" and browse to your desktop for the DevBox file.
5. Follow the on-screen instructions until your virtual machine is finished installing.
6. Launch Predix Devbox.

####Creating YML File
7. Open gedit in Devbox (Applications > Accessories > gedit Text Editor).
8. Paste the following text:
```applications:
  - name: APP_NAME_GOES_HERE
    buildpack: staticfile_buildpack 
    #path: dist
    memory: 64M
    stack: cflinuxfs2
```
9. Change APP_NAME_GOES_HERE to your desired application name.
10. Save the file as ```manifest.yml``` into the directory that contains your application and close gedit.

####Push Application to Predix
11. Direct the terminal to your folder that contains your project code and manifest file.
12. Log into your Predix account using the following command: 
```cf login -a https://api.system.aws-usw02-pr.ice.predix.io```
13. Enter your Predix account email and password. You should see the terminal respond with
```
Email> <your_predix_login>
Password> <your_predix_password> 
Authenticating...OK 
Targeted org <your_predix_org> 
Targeted space dev     
API endpoint: https://api.system.aws-usw02-pr.ice.predix.io (API version: 2.28.0)   
User: <your_predix_login> 
Org:  <your_predix_org>  
Space: dev
```
14. Push your app to Predix using the command: ```cf push```
15. You should see an output like this:
```
Starting app Predix-HelloWorld_WebApp-<YourAppName> in org YourAppName / space dev as YourAppName...
-----> Downloaded app package (4.0K)
-----> Downloaded app buildpack cache (4.0K)
-------> Buildpack version 1.2.1
grep: Staticfile: No such file or directory
-----> Using root folder
-----> Copying project files into public/
-----> Setting up nginx
grep: Staticfile: No such file or directory
-----> Uploading droplet (11M)
 
1 of 1 instances running
 
App started
 
OK
 
App Predix-HelloWorld_WebApp-<YourAppName> was started using this command `sh boot.sh`
 
Showing health and status for app Predix-HelloWorld_WebApp-<YourAppName> in org YourAppName / space dev as YourAppName...
OK
 
requested state: started
instances: 1/1
usage: 64M x 1instances
urls: APP_NAME_HERE.run.aws-usw02-pr.ice.predix.io
last uploaded: Fri Oct 30 21:10:50 UTC 2015
stack: cflinuxfs2
buildpack: predix_openresty_buildpack
```
16. Your app is now hosted on Predix! Open your browser and paste the link found under "urls" in the above output. Be sure to add ```https://``` before you paste the URL.

####(Optional) Cloning Existing Projects on Github to Deploy to Predix
1. Determine the direct URL to your Github-hosted project.
2. Open your terminal and perform the following command: 
```git clone https://www.github.com/YOUR-REPO-NAME-HERE```
3. Add the ```manifest.yml``` file to the folder that was created on your local machine.
4. Repeat the above steps to push the app to Predix.

-------

References:
+ [Hello World : A simple HTML page](https://www.predix.io/resources/tutorials/tutorial-details.html?tutorial_id=1475&tag=1719&journey=Hello%20World&resources=1475,1569,1523)
+ [DevBox Tutorial](https://www.predix.io/services/other-resources/devbox.html)
+ [Experience Predix, Use Predix](https://www.predix.io/resources/tutorials/tutorial-details.html?tutorial_id=1630)
+ [Developer Resources](https://www.predix.io/resources/tutorials)
