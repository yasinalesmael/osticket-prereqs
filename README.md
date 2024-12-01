<p align="center">
<img src="https://i.imgur.com/mNVi2e8.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10 Pro </b> (22H2), at least 2vCPUs, 8GB RAM

<h2>List of Prerequisites</h2>

- <b>PHP manager for IIS</b> - ensures PHP is correctly configured to run IIS
- <b>Rewrite module </b> - facilitates URL rewriting and redirect users to URLs
- <b>VC_redist.x86</b> (redistributable) - osTicket relies on libraries that are part of Microsoft Visual C++ and ensures the program runs smoothly
- <b>MySQL</b> - for storing data into databases
- <b>HeidiSQL</b> - interface for accessing MySQL 


<h2>Installation Steps</h2>
<p>
Once the Windows 10 VM has been set up in Azure, log into the machine with your credentials. It is best to create a notepad and save a copy of any credentials used along the way for this lab, as there'll be many.
Within the VM, open the Microsoft Edge web browser and download <a href= https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD>osTicket-Installation-Files.zip</a>. Extract the files and you should see the following.

</p>
<br />

<p>
<img src="https://i.imgur.com/6ZlXmrF.png" height="80%" width="80%" alt="extracted osticket zip file"/>
</p>


<p>
Now we'll need to enable Internet Information Services. You can search for Control Panel in the search bar at the bottom, then click Uninstall a Program, then Turn Windows features on or off, then check the box next to Internet Information Services. We'll also need to enable CGI under World Wide Wide Services -> Application Development Features.
</p>
<br />

<p>
<img src="https://i.imgur.com/CdojXsp.png" height="80%" width="80%" alt="enable IIS and CGI"/>
</p>
<br/>
<p>
Once that's done, we can install the PHP manager for IIS. Open on the file and click OK to all the default selections. Do the same thing for the rewrite modules (rewrite_amd64 file).
</p>
<img src="https://i.imgur.com/Uh4Zwlj.png" height="80%" width="80%" alt="install php manager and rewrite"/>

<br />

<p>
Now we'll create a directory in C:\ called PHP, basically C:\PHP. Click on the folder at the bottom the Taskbar or search for File Explorer. This is so that we can extract the zipped PHP folder into this new directory and allow osTicket to work with PHP.
</p>
<p>
  <img src="https://i.imgur.com/BCMLUId.png" height="80%" width="80%" alt="extract php to c php"/>
</p>
<br/>

<p>
Next install the redistributable and accept all defaults. Then install MySQL, select Standard Configuration and then enter root and root as the username and password. This is just for simplicity and you'd likely use a stronger password in real life.
  
</p>
<p>
  <img src="https://i.imgur.com/dbDt0um.png" height="50%" width="50%" alt="install redistr and mysql"/>
</p>
<br/>

<p>
Now open Internet Information Services, type IIS in the search bar and then Run as administrator. Click on PHP manager then register new PHP version. Select C:\PHP\php-cgi.exe
  
</p>
<p>
  <img src="https://i.imgur.com/3twI19f.png" height="80%" width="80%" alt="configure PHP new version in PHP manager"/>
</p>
<br/>

<p>
Reload IIS by clicking stop then start on the right hand side. This will help load the new PHP version.
</p>
<p>
  <img src="https://i.imgur.com/iO7K6aO.png" height="30%" width="30%" alt="reload IIS"/>
</p>
<br/>

<p>
Extract the osticket zipped folder and move the extracted upload folder into C:\inetpub\wwwwroot, then rename upload to osTicket (it must be exact).
  
</p>
<p>
  <img src="https://i.imgur.com/xJw174Y.png" height="80%" width="80%" alt="extract osticket zipped folder and move to wwwroot"/>
</p>
<br/>

<p>
Reload IIS again. On the left side pane, go to Sites, click the down arrow until you reach osTicket and then click on Browse in the right side pane, then you should get this.
</p>
<p>
  <img src="https://i.imgur.com/4ahLEvm.png" height="80%" width="80%" alt="osticket landing page"/>
</p>
<br/>
<p>
Now we'll need to enable some extensions. Go back to the osTicket folder on the left side pane and then click on PHP manager in the middle pane. Click on Enable or disable an extension and you'll need to enable php_imap.dll, php_intl.dll and php_opcache.dll. Refresh the osTicket webpage and it should be updated.
</p>
<p>
  <img src="https://i.imgur.com/mPryTWa.png" height="80%" width="80%" alt="updated osticket landing page"/>
</p>
<br/>
<p>
Now we have to rename C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php to C:\inetpub\wwwroot\osTicket\include\ost-config.php. Then we'll need to change permissions for this file. Right click on this and then Properties -> Security tab -> Advanced -> Disable inheritance (remove option) -> Add -> Select a principal -> Type everyone in the box -> Check names -> OK. Make sure you click on Full control as well.
</p>
<p>
  <img src="https://i.imgur.com/1IdFy6F.png" height="80%" width="80%" alt="ost config permissions"/>
</p>
<br/>
<p>
Now back to osTicket on the browser, click Continue and fill in the details that you want to use as login and password for the helpdesk system. The only caveat is the MySQL database name is osTicket and the username and password must be root and root. Before clicking continue on this, go back to the original extracted folder and install HeidiSQL. Accept all defaults and when it comes to creating a new session, select new and then login into the sql database with root and root credentials. Then right click on Unnamed -> Create new -> Database. The name must be exactly osTicket.
</p>
<p>
  <img src="https://i.imgur.com/Lfw0PXJ.png" height="80%" width="80%" alt="heidisql"/>
  <img src="https://i.imgur.com/pWKEjjz.png" height="80%" width="80%" alt="create new database in heidisql"/>
</p>
Continue with the installation of osTicket in the browser by clicking Install Now. You should now seeing the page telling you that osTicket is finally installed and all the links to login into the osTicket as a general user (http://localhost/osTicket) or as staff (http://localhost/osTicket/scp).
<br/>
<p>
   <img src="https://i.imgur.com/CBKO7Qs.png" height="80%" width="80%" alt="osticket installed"/>
</p>
