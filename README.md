# Backing Up Your WordPress Site

## Description

In this lesson you will learn of the fact that your WordPress.org self-hosted website contains physical files and a database, both of which need to be backed up on a regular schedule. In addition, Backups should also be performed before any core, plugin, or theme updates, as well as before installing new plugins. While there are many free and commercial backup plugins available to backup both components of your site, you should also know how to do a manual backup of your database using [PHPMyAdmin](http://codex.wordpress.org/phpMyAdmin), as well as how and which files to backup using an SFTP client such as [Filezilla](http://codex.wordpress.org/Using_FileZilla) or [Cyberduck](https://cyberduck.io/?l=en). This one-hour lesson will teach you how you can manually backup your files and your database of your self-hosted WordPress.org website and also provide best practices for storing and maintaining your backups.  

## Objectives

After completing this lesson, you will be able to:

*   Identify the files of a WordPress installation.
*   Perform a backup of physical files.
*   Identify and be aware of the difference between FTP and SFTP.
*   Export the database using [PHPMyAdmin](http://codex.wordpress.org/phpMyAdmin).
*   Describe the best practices of maintaining and storing backup files.

## Prerequisite Skills

You will be better equipped to work through this lesson if you have experience in and familiarity with:

*   SFTP hosting credentials: hostname, port, username, and password
*   How to use an basic SFTP client, such as [Filezilla](http://codex.wordpress.org/Using_FileZilla) or Cyberduck
*   Access to your hosting panel's [PHPMyAdmin](http://codex.wordpress.org/phpMyAdmin) or database administration

## Assets

*   An example WordPress installation with content
*   An SFTP client such as [Filezilla](http://codex.wordpress.org/Using_FileZilla), along with credentials
*   Access to hosting control panel such as cPanel or Plesk, along with credentials
*   [PHPMyAdmin](http://codex.wordpress.org/phpMyAdmin) running on the server

## Screening Questions

*   Do you have a self-hosted WordPress.org website (vs. WordPress.com website)?
*   Do you have SFTP credentials to your website? (ask your web h0st)
*   Do you have access to a hosting control panel, such as cPanel or Plesk? (ask your web host)
*   Do you have access to run PHPMyAdmin on your server? (ask your web host)

## Teacher Notes

The teacher should perform a step-by-step demo of how to backup of the WordPress files using Filezilla, then demonstrate how to backup the WordPress database using PHPMyAdmin. Following the demo, the teacher should go over best practices for storing and maintaining backups. Once all complete, the students should be invited to create their own backup of files and database and answer the quiz questions about backups. Additional information about backing up WordPress can be found on the codex at the following locations:

*   [http://codex.wordpress.org/WordPress_Backups](http://codex.wordpress.org/WordPress_Backups),
*   [http://codex.wordpress.org/Backing_Up_Your_Database](http://codex.wordpress.org/Backing_Up_Your_Database)
*   [http://codex.wordpress.org/WordPress_Backups#Backing_Up_Your_WordPress_Site](http://codex.wordpress.org/WordPress_Backups#Backing_Up_Your_WordPress_Site)

## Hands-on Walkthrough

This hands-on walkthrough will show you how to backup your WordPress.org website files and database manually. The website files include the WordPress core application files, the theme files, the plugin files, and all media that you have uploaded to your WordPress installation. The database file that we will create will contain all of your website's content: posts, pages, CPTs, menus, widgets, theme settings, plugin settings, and WordPress configuration settings. You will need to backup both the files and the database to backup your entire WordPress site.

### 1) Backing up your site's files

#### Difference Between FTP and SFTP

It is important that when you connect and transfer your files that you do so in a secure way that will not expose your password to anyone on the network. For this reason, we recommend using SFTP (Secure File Transfer Protocol) instead of FTP (File Transfer Protocol), as it will encrypt your password before sending it out over the network. Most hosts may offer SFTP with either the same or a different set of credentials, so be sure to check with them regarding your setup if you are unsure.

#### Configuring Filezilla

Locate and open Filezilla. You will see the following screen, click on the icon indicated to open the Site Manager.

![filezilla-1](/images/filezilla-1.png)

In the Site Manager dialog box that opens, enter the credentials you received from your web host as follows, make sure to select SFTP as your Protocol and select the Logon Type: Normal. Some web hosts provide a port number; if so, enter it under Port, but it most cases, it is ok to leave it blank. 

[![](/images/filezilla-2.png)

#### Connect to your server

Click the "Connect" button at the bottom of the dialog box. Upon successful connection, you should see a list of files on the remote server that looks similar to below. 

[![](/images/filezilla-31.png)

#### Identify WordPress files

Depending on your individual setup, your WordPress site may be located in a folder sometimes called "**html"** , "**blog**", or it may be readily visible once you connect. Look for the following folders: **wp-admin**, **wp-content**, and **wp-includes**. These are the folders that make up your WordPress installation. In the top folder that contains those folders, you will also find the files that make up your WordPress core installation. We will need to copy all of these folders and files.

#### Create a local folder to hold your backup

In Filezilla, the left side of the window contains your local files on your computer. You will need to browse to the desktop of your PC or Mac: 

[![](/images/filezilla-4.png)

When you click on the Desktop folder, the pane below will show all of the current folders and files. When you right-mouse-click the Desktop folder, you will be presented with a list of options, select, "**Create directory**". 

[![](/images/Filezilla5.png) 

Enter the name as "**backup-2015-02-02**" after the path to your desktop, using today's date. This will help you to identify different backups from different days. Click the "**OK**" button. 

[![](/images/filezilla-6.png)

Scroll down in the local files menu and locate the folder you just created, double-click it to select it. You should see that there are no files in this directory. 

[![](/images/filezilla-7.png)

#### Copy WordPress files to the local folder

There are several ways in which you may download your WordPress files, the easiest way is to click on the remote server pane, hit Ctrl+A (PC) or Cmd+A (Mac) to select all the files on the remote server, and then pull them over to the empty pane under your desktop folder than you created. This will begin the download process which may take a few minutes depending on the size of your installation. 

![](https://raw.githubusercontent.com/wptrainingteam/contributor-resources/master/images/icon-help.png) Missing image below

![backingup.gif](http://make.wordpress.org/training/files/2015/01/backingup.gif) 

The bottom-most transfer status pane will appear blank after the files have all been transferred, and they will have been copied to your backup folder that you created previously. Congratulations, you have backed up your site files! You are now halfway done to creating a full backup.

### 2\. Backing up the Database

In addition to your site's files, your website is also comprised of a database that stores all of your content and settings. In this demonstration, you will be shown how to export your database to an .SQL file.

#### View wp-config.php to obtain database name

Connect to SFTP,  browse to the root of your WordPress installation, right-mouse click on wp-config.php, and select View/Open. Scroll down to the the DB_NAME field, and note the DB_Name, DB_USER, and DB_PASSWORD fields. These fields contain the information you will need to logon to PHPMyAdmin. 

[![](/images/wp-config.png)

#### Logon to PHPMyAdmin

Obtain the URL to logon to PHPMyAdmin from your web hosting provider. IT may accessible through cPanel or Plesk, depending on your individual web hosting provider. Enter in the username and password to logon, which is found in the wp-config.php file.

#### Select the correct database

On the left, you will see a list of databases. Select the database that corresponds with the one indicated in wp-config.php. Once selected, you will see a list of tables and command tabs on the right side. 

![](https://raw.githubusercontent.com/wptrainingteam/contributor-resources/master/images/icon-help.png) Missing image below

[![](https://make.wordpress.org/training/files/2015/01/phpmyadmin-1024x359.png)](https://make.wordpress.org/training/files/2015/01/phpmyadmin.png)

#### Export the data to an .SQL file in your local folder

[![](/images/phpmyadmin-export.png)

## Exercises

**Create a backup of your site's files** Following the steps as illustrated in the demonstration,  backup your site's files to a folder on your desktop.

*   Download and install Filezilla, if needed.
*   Configure the connection settings with credentials from your host.
*   Create a folder named, "**backup-2015-02-02**" on your desktop using today's date.
*   Download all the files and folders that makeup your WordPress installation to this folder
*   Teacher should verify the correct folders and files have been downloaded.

**Create a backup of your site's database** Following the steps as illustrated in the demonstration,  backup your site's database and save to the same folder created previously on your desktop.

*   C

## Quiz

**Question:** When connecting to your server to download files, you should always use SFTP instead of FTP.

1.  True
2.  False

**Answer** 1\. True. Using SFTP encrypts your username and password so it cannot be viewed by others on the network. **Question:** If you only backup your files, what will be missing from your backup?

1.  WordPress application files
2.  All of your content and settings
3.  Theme and template files
4.  Plugins
5.  All of the above

**Answer:** 2\. All of your content and settings: posts, pages, CPTs, menus, widgets, and configuration settings are all part of the database, which also needs to be backed up. **Question:** What is the first thing you should do after opening Filezilla to backup your files?

1.  Download the folders
2.  Download the files
3.  Open the connection dialog and connect
4.  View the remote server files
5.  All of the above

**Answer:** 3\. Open the connection dialog, enter your credentials, then click connect to connect to the remote server. Once connected, you will be able to view the folders and files on the server and be able to download them. **Question:** Which files and folders should you download to make a complete backup of the WordPress files?

1.  wp-admin folder
2.  wp-content folder
3.  wp-includes folder
4.  All of the files at the root of the WordPress folder
5.  All of the above

**Answer:** 5\. All of the above. You must download the entire wp-admin, wp-includes, wp-content folders and all of root files in the WordPress folder.

## Additional Resources

[WordPress Backups](https://codex.wordpress.org/WordPress_Backups) @ Codex
