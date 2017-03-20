Web.config, Azure, Web Forms app, suicidal vibes.
<img src = "https://static.spiceworks.com/shared/post/0003/6524/IMG_ThePush_2014-0505_SecureAllTheThings.jpg">

**What?**

Currently I'm working on my university team project called <a href = "https://github.com/d1mnewz/DaphneBot">DaphneBot</a>. Simply saying, that's a Slack chat bot that collects statuses of tasks from developers, saves it into database and publishing into some specified document.  It's hosted as Azure App Service for now, feel free to take a <a href = "http://helloteam.azurewebsites.net/">look</a>.

Firstly we decided to add Web.config with connection string, MicrosoftAppId, MicrosoftAppPassword to .gitignore to secure our credentials. That went almost well. No, it went totally well: we had local Web.config on our machines that wasn't pushing to our public repository.

But at some point our team faced that we need to make continuous deployment on Azure.
Here goes some weird shit: if you link your repository with your app service on Azure, it must have Web.config. At first I just removed it from .gitignore, but it wasn't my best decision, right? Then I started googling around, looking for some pre-made StackOverflow solution.
Well, our <a href = "https://github.com/volodymyr-mykhailyk">mentor</a> suggested me to look for some environment variables on our Azure host. It seemed legit for me, so here is my solution.


**Again what?**

OK. You have Web.config, App Service on Azure and task about credentials security on continuous deployment.

What you need to do:
* Read about environment variables on Azure <a href = "https://blogs.msdn.microsoft.com/stuartleeks/2015/08/10/azure-api-apps-configuration-with-environment-variables/">here</a>
* Go to your app panel on <a href = "portal.azure.com/#">Azure portal</a> -> Application Settings -> App settings & Connection strings
* Paste your credentials from app settings & connection strings from web.config in these sections

* As result you should get something like this:
 <img src = "http://joxi.ru/BA0OxQkCWJj82y.png"/>
* Notice that your entity framework connection string should be selected as **Custom**, not __SQL Database__.
* Also have a look at your entity framework connection string: if it has some '&quote ;' (no space) symbols, you must replace them with single quote symbols ('). As final your connection string for EntityFramework here must look like this:

<q> __metadata=res://*/DaphneModel.csdl|res://*/DaphneModel.ssdl|res://*/DaphneModel.msl;provider=System.Data.SqlClient;provider connection string='data source=tcp:daphnebot.database.windows.net,1433;initial catalog=DaphneBot;persist security info=False;user id=user;password=pword;multipleactiveresultsets=True;connect timeout=30;encrypt=True;trustservercertificate=False;App=EntityFramework';__</q>
**Now what?**

Now you are good to go with continuous deployment, all of your secure web.config data will be stored on host as environment variables. Actually, you don't even need to change something in your release code because these variables overwrite existing ones. So if you are pushing and publishing with web.config where something is already defined, it is going to be overwritten. And e.g. the connection string will be taken from environment variables.

For now we have a .gitignore with Web.config included, so we have to store current version on our local machines, but it won't be included in commits. When master updates, Azure via continuous deployment publishing updates to our App Service, so we don't have to worry about publishing at all, we are always up to date.

Seems good, right?  
