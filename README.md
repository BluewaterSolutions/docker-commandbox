Official Commandbox Dockerfiles [![Build Status](https://travis-ci.org/Ortus-Solutions/docker-commandbox.svg)](https://travis-ci.org/Ortus-Solutions/docker-commandbox)
=========================

This is the repository for official Dockerfiles for Commandbox

## How it works

The Docker files in this repository can be used to create your own custom Docker container for running CFML applications on CommandBox.   Leveraging CommandBox allows you to configure your entire CFML engine environment from a single `server.json` file in the root of your project.

About CommandBox
================

*CommandBox* is a standalone, native tool for Windows, Mac, and Linux that will provide you with a Command Line Interface (CLI) for developer productivity, tool interaction, package management, embedded CFML server, application scaffolding, and some sweet ASCII art. It seamlessly integrates to work with any of our *Box products but it is also open for extensibility for any ColdFusion (CFML) project as it is also written in ColdFusion (CFML) using our concepts of CommandBox Commands.  It tightly integrates with our contribution community; ForgeBox, so developers can share modules world-wide.

Learn more about CommandBox at https://www.ortussolutions.com/products/commandbox

What CommandBox Can Do 
=======================

CommandBox allows you to configure your entire CFML engine environment from a single file in the root of your project.  For more information on how to leverage CommandBox in developing and deploying your applications, see the [official documentation](https://ortus.gitbooks.io/commandbox-documentation/). 

Current CFML engines supported are:

- Lucee:  4+ & 5+
- Adobe Coldfusion 10+

You may also specify a custom WAR for deployment, using the `server.json` configuration.

Usage
================

This section assumes you are using the [Official Docker Image](https://hub.docker.com/r/ortussolutions/commandbox/)

By default, the directory `/app` in the container is mapped as Commandbox home.  To deploy a new application, first pull the image:

```
docker pull ortussolutions/commandbox
```

Then, from the root of your project, start with

```
docker run -p 8080:8080 -p 8443:8443 -v "/path/to/your/app:/app" ortussolutions/commandbox 
```

By default the process ports of the container are 8080 (insecure) and 8443 (secure - if enabled in your `server.json`) so, once the container comes online, you may access your application via browser using the applicable port (which we explicitly exposed for external access in the `run` command above).  You may also specify different port arguments in your `run` command to assign what is to be used in the container and exposed.  This prevents conflicts with other instances in the Docker machine using those ports:

```
docker pull -expose-list 80 443 -e "PORT=80" -e "SSL_PORT=443" -v "/path/to/your/app:/app" ortussolutions/commandbox
```

To create your own, customized Docker image, use [our Dockerfile repository](https://github.com/Ortus-Solutions/docker-commandbox) as the baseline to begin your customizations.

Environment Variables
=====================

The CommandBox Docker image support the use of environmental variables for the configuration of your servers.  Specifically, the image includes the [`cfconfig` CommandBox module](https://www.forgebox.io/view/commandbox-cfconfig), which allows you to provide custom settings for your engine, including the admin password.

* `$PORT` - The port which your server should start on.  The default is `8080`.
* `$SSL_PORT` - If applicable, the ssl port used by your server The default is `8443`.
* `$CFENGINE` - Using the `server.json` syntax, allows you to specify the CFML engine for your container
* `$HEALTHCHECK_URI` - Specifies the URI endpoint for container health checks.  By default, this is set `http://127.0.0.1:${PORT}/` at 1 minute intervals with 5 retries and a timeout of 30s 
* `$cfconfig_[engine setting]` - Any environment variable provided which includes the `cfconfig_` prefix will be determined to be a `cfconfig` setting and the value after the prefix is presumed to be the setting name.  The command `cfconfig set ${settingName}=${value}` will be run to populate your setting in to the `$SERVER_HOME_DIRECTORY`.
* `$CFCONFIG` - A `cfconfig`-compatible JSON file may be provided with this environment variable.  The file will be loaded and applied to your server.  If an `adminPassword` key exists, it will be applied as the Server and Web context passwords for Lucee engines
* `$SERVER_HOME_DIRECTORY` - When provided, a custom path to your server home directory will be assigned.  By default, this path is set as `/root/serverHome` ( _Note: You may also provide this variable in your app's customized `server.json` file_ )

Issues
================

Please submit issues to our repository: [https://github.com/Ortus-Solutions/docker-commandbox/issues](https://github.com/Ortus-Solutions/docker-commandbox/issues)

## LICENSE
Apache License, Version 2.0.

<hr/>

#### HONOR GOES TO GOD ABOVE ALL
Because of His grace, this project exists. If you don't like this, then don't read it, its not for you.

>"Therefore being justified by faith, we have peace with God through our Lord Jesus Christ:
By whom also we have access by faith into this grace wherein we stand, and rejoice in hope of the glory of God.
And not only so, but we glory in tribulations also: knowing that tribulation worketh patience;
And patience, experience; and experience, hope:
And hope maketh not ashamed; because the love of God is shed abroad in our hearts by the 
Holy Ghost which is given unto us. ." Romans 5:5

#### THE DAILY BREAD
 > "I am the way, and the truth, and the life; no one comes to the Father, but by me (JESUS)" Jn 14:1-12
