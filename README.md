Graphity-Server
===============

Welcome to the Graphity Server project!

We would like to introduce you with a guide showing you how to pull the Graphity Server to your local repository, make changes with your IDE and in future how to configure and finally run it.


<h2>Dependencies</h2>

Make sure you have installed and configured:
+ [Maven](#1-install-maven-305) (3.0.5)
+ [Java JDK 1.7](#2-install-java-jdk-17)
+ [Eclipse](#4-install-eclipse-classic-422-juno) (Classic 4.2.2 'Juno')
+ [m2e](#5-install-maven-plugin-for-eclipse-m2e)
+ [EGit](#6-install-git-plugin-for-eclipse-egit)

<h2>Pull Graphity Server</h2>

At first we have to pull the remote repository.  
[File > Import > Git > Projects from Git]

Choose 'URI' in the next step.  
Use the URI provided by GitHub.com which is  
https://github.com/sebschlicht/Graphity-Server.git

for my repository. The value may change if you fork it.

If you have not configured SSH yet choose the HTTPS connection and type in your authentication information.

Select the master branch and set the destination directory which can be the default value of course.  
For me it is 'home/sebschlicht/git/Graphity-Server/'

Now you have to select the wizard. Choose 'Import as general project' and step on.  
Change the project name if you want to and finish the import.

The code has been downloaded, but it is not a Maven project yet.  
To change this [right-click the project > Configure > Convert to Maven Project].

The project should have changed now and should be recognized as a Java project having a source folder.


<h1>Detailed guide</h1>

For beginners and those who are not sure if they have installed the necessary components correctly we have created a detailed guide how to install and configure all the components.

This guide assumes that your operating system is Ubuntu x86.<br>For other operating systems the steps may be slightly different.


<h2>1. Install Maven (3.0.5)</h2>

__If you have installed Maven already, please proceed with step 2: [Install Java JDK 1.7](#2-install-java-jdk-17)__

Download Maven from http://maven.apache.org/download.cgi#Installation using the Maven 3.0.5 Binary tar.gz first.

Now start a new terminal. [Ctrl + Alt + T]

Switch to the downloads directory using  
`cd $HOME/Downloads`

If you type  
`ls`

you will recognize the file downloaded before. It's name should be ‘apache-maven-3.0.5-bin.tar.gz'

Unpack the archive using  
`tar -zxf apache-maven-3.0.5-bin.tar.gz`

If you type  
`ls`

again you will recognize a new folder 'apache-maven-3.0.5' that has been created.
As suggested in the installation instructions at the download website of Maven we move this folder to /usr/local. If we want to do so we have to create a directory first.

Type in  
`sudo mkdir /usr/local/apache-maven`

The 'sudo' command is necessary while a user account does not have the permissions to make changes in this directory.

Now move the unpacked Maven by typing in  
`sudo mv apache-maven-3.0.5 /usr/local/apache-maven/`

Make sure that the directory has been moved properly:  
<pre><code>cd /usr/local/apache-maven/  
ls</code></pre>

You should now see the directory 'apache-maven-3.0.5'.


<h2>2. Install Java JDK 1.7</h2>

__If you have installed the Java JDK already, please proceed with step 3: [Set environment variables](#3-set-environment-variables)__

To run maven we need to have the Java JDK installed.  
Download it from http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html

Make sure to accept the license agreement and then download the JDK file matching your system.  
For me it is the file for Linux x86 (tar.gz).

Source:  
http://askubuntu.com/questions/55848/how-do-i-install-oracle-java-jdk-7

Switch to the downloads directory again:  
<pre><code>cd $HOME/Downloads  
ls</code></pre>

Unpack the new archive file using  
`tar -xvf jdk-7u17-linux-i586.tar.gz`

Typing in  
`ls`

should make you able to see the new folder 'jdk1.7.0_17'.  
Now let's move this folder to the library directory.

At first create the target directory using  
`sudo mkdir /usr/lib/jvm`

Now move the directory:  
`sudo mv ./jdk1.7.0_17 /usr/lib/jvm/jdk1.7.0`

Install the important executables using  
<pre><code>sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.7.0/bin/java" 1  
sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.7.0/bin/javac" 1  
sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/lib/jvm/jdk1.7.0/bin/javaws" 1</code></pre>

Set the correct permissions via  
<pre><code>sudo chmod a+x /usr/bin/java  
sudo chmod a+x /usr/bin/javac  
sudo chmod a+x /usr/bin/javaws</code></pre>


You can now check for a proper installation of the Java JDK by typing in  
`java -version`


<h2>3. Set environment variables</h2>

__If you have set the environment variables already, please proceed with step 4: [Install Eclipse](#4-install-eclipse-classic-422-juno)__

Environment variables exported via Terminal will be valid for one session only.  
To create them permanently we need to add them to the ~/.pam_environment file.  
You may have to create this file at first.

Sources:  
https://help.ubuntu.com/community/EnvironmentVariables  
http://askubuntu.com/questions/125421/how-to-open-pam-environment

It should contain the following lines according to the variables set above:  
>M2_HOME DEFAULT=/usr/local/apache-maven/apache-maven-3.0.5  
>M2 DEFAULT=${M2_HOME}/bin  
>JAVA_HOME DEFAULT=/usr/lib/jvm/jdk1.7.0  
>PATH DEFAULT=${JAVA_HOME}/bin:${M2}:${PATH}  

__Logout and login again to have the changes take effect.__

You can verify a proper installation of Maven now via  
`mvn --version`


<h2>4. Install Eclipse (Classic 4.2.2 'Juno')</h2>

__If you have installed Eclipse already, please proceed with step 5: [Install Maven Plugin for Eclipse](#5-install-maven-plugin-for-eclipse-m2e)__

Firstly download Eclipse for Linux: http://www.eclipse.org/downloads/?osType=linux

Switch to the download directory:  
<pre><code>cd $HOME/Downloads  
ls</code></pre>

Source:  
http://colinrrobinson.com/technology/install-eclipse-ubuntu/

Unpack the Eclipse archive:  
`tar xzf eclipse-SDK-4.2.2-linux-gtk.tar.gz`

Eclipse has now been unpacked to the directory ‘eclipse’.

Now move Eclipse to the ‘opt’ folder and set owner and permissions:  
<pre><code>sudo mv eclipse /opt/  
cd /opt/  
sudo chown -R root:root eclipse  
sudo chmod -R +r eclipse</code></pre>

Create an executable link for Eclipse:  
<pre><code>sudo touch /usr/bin/eclipse  
sudo chmod 755 /usr/bin/eclipse</code></pre>

Now create a start script by typing in  
`sudo nano /usr/bin/eclipse`

and fill the script with  
>\#!/bin/sh  
>\#export MOZILLA_FIVE_HOME="/usr/lib/mozilla/"  
>export ECLIPSE_HOME="/opt/eclipse"  
>$ECLIPSE_HOME/eclipse $*

Save the file with Ctrl + O, commit the file name by pressing Enter and return to the terminal via Ctrl + X.

Now create a GNOME menu item:  
`sudo nano /usr/share/applications/eclipse.desktop`

Fill the item with  
>[Desktop Entry]  
>Encoding=UTF-8  
>Name=Eclipse  
>Comment=Eclipse IDE  
>Exec=eclipse  
>Icon=/opt/eclipse/icon.xpm  
>Terminal=false  
>Type=Application  
>Categories=GNOME;Application;Development;  
>StartupNotify=true  

Save the file and close nano as described before.

Now launch eclipse once via  
`/opt/eclipse/eclipse -clean &`

You may want to lock Eclipse to your launcher by right-clicking at the Eclipse icon in the launcher bar at the left of the screen and checking ‘Lock to Launcher’.


<h2>5. Install Maven Plugin for Eclipse (m2e)</h2>

__If you have installed m2e already, please proceed with step 6: [Install Git Plugin for Eclipse](#6-install-git-plugin-for-eclipse-egit)__

Source:  
http://stackoverflow.com/questions/2524958/eclipse-3-5-1-galileo-with-ubuntu-9-10-karmic-busted-can-not-install-maven2

Start Eclipse and click [Help > Install new Software].

Add and use the Eclipse update URL  
http://download.eclipse.org/releases/juno

and select ‘m2e - Maven Integration for Eclipse’ which can be found in ‘General Purpose Tools’.

Do not use the URL suggested by Maven while there are dependencies that may not be fulfilled yet.  
Step on, accept the license agreement and start the installation via ‘Finish’.

Restart Eclipse after the installation.


<h2>6. Install Git Plugin for Eclipse (EGit)</h2>

Open a terminal and install git first.  
`sudo apt-get install git`

Now open Eclipse.  
`eclipse`

Install the plugin from the following Eclipse update URL like mentioned in the previous step:  
http://download.eclipse.org/egit/updates

and select ‘Eclipse EGit’ which can be found under ‘Eclipse Git Team Provider’.

Step on, accept the license agreement and start the installation via ‘Finish’.

Restart Eclipse after the installation.


<h2>Congratulations</h2>

You do fulfill all dependencies now to access the Graphity Server project!  
Scroll to the top of the page and pull the project as described.

You can now build the project using Maven.  
Open a new terminal and switch to the project directory:  
`cd $HOME/git/Graphity-Server/`

Build the project:  
`mvn package`
