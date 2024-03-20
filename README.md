<h1> Detecting and representing failed remote desktop logins (RDP) on world map on Microsoft Azure using Sentinel SIEM </h1>

<h2>Description</h2>
In this project I setup a virtual machine, log analytics workspace and a Security Information and Event Management (SIEM) on Microsoft Azure using the student free trial offered by Microsoft. Then I gathered the failed brute force attacks on the VM over time and then use log analytics workspace and sentinel to display the locations of the attacks on a world map. <br>

<h2>Languages Used</h2>

- <b>PowerShell:</b> Extract RDP failed logon logs from Windows Event Viewer 

<h2>Utilities Used</h2>

- <b>ipgeolocation.io:</b> IP Address to Geolocation API

<h2>Project walk-through:</h2>
We begin this project by creating a free trial of Microsoft Azure's services for a month. Once we complete that we create a windows VM on Azure, followed by a log analytics workspace and then setup our SIEM which is sentinel. Once we have set these up we connect the log analytics workspace to our VM.<br />
One thing to note is that when setting up our VM, we have to configure the inbound rules of the VM so as to get a lot of traffic to our VM. This process is depicted below:
<br /><br />
<p align="center">

<img src="https://i.imgur.com/ISVtKsJ.png" height="80%" width="80%" alt="Task 1"/>
</p>
<br /> 
Creating the log analytics workspace:
<br /><br />
<p align="center">

<img src="https://i.imgur.com/GwvwbtD.png" height="80%" width="80%" alt="Task 1"/>
</p>
<br /> 
Creating the SIEM (sentinel) :
<br /><br />
<p align="center">

<img src="https://i.imgur.com/wEyOs9j.png" height="80%" width="80%" alt="Task 1"/>
</p>
<br /> 
Once we have completed these initial tasks, we move on to connecting to our VM using the Remote Desktop application on windows and logging in with our credentials:
<br /><br />

<p align="center">

<img src="https://i.imgur.com/ZRe8Icr.png" height="80%" width="80%" alt="Task 1"/>
</p>
<br /> 

Once we are logged in to our VM, we need to go to the windows firewall and deactivate it so as to not filter any traffic trying to brute force our VM: 
<br />
<p align="center">

<img src="https://i.imgur.com/mHQARo0.png" height="80%" width="80%" alt="Task 1"/>
</p>
<br /> 

Here is what the event viewer looks like in our VM. This is where we will collect the data of the failed RDP logins using a Powershell script: 
<br />
<p align="center">

<img src="https://i.imgur.com/3Gs7kt3.png" height="80%" width="80%" alt="Task 1"/>
</p>
<br /> 

Now before we implement the powershell script we need an API key to a website (ipgeolocation.io) which will convert the IP addresses we collect into latitudes and longitudes for us to plot on a map:
<br /><br />
<p align="center">

<img src="https://i.imgur.com/xFim7qK.png" height="80%" width="80%" alt="Task 1"/>
</p>
<br /> 

Now that we have our API key, I created a Powershell script using resources on youtube to do these tasks on the VM: 
- Get the API key
- Filter out the failed RDP events from the Event Viewer
- Create a log file
- Create a loop to constantly check the Event Viewer Logs
- Categorize the data of the failed RDP logins into different columns
- Pull data from the geo location website
- Write all the information to the log file.
<br />
This is what the powershell window will look like when the script is ran: 
<br /><br />
<p align="center">

<img src="https://i.imgur.com/EbuH6X9.png" height="80%" width="80%" alt="Task 1"/>
</p>
<br />

Small sidenote, I am using sample data from a previous person who completed a similar project to use for my logs, as we need to run the VM for a long period to collect data. Since I was short on time I used some sample data.

<br />
Now once we are done with all of this, we go back to Log Analytics Workspace on our microsoft azure portal and using the logs that the Powershell script has generated we create a table in Azure: 
<br /><br />
<p align="center">

<img src="https://i.imgur.com/reOMO5l.png" height="80%" width="80%" alt="Task 1"/>
</p>
<br />

Finally we have one last step which is to create a workbook on Sentinel which takes the table from our Log Analytics Workspace and plots it on a world map: 
<br /><br />
<p align="center">

<img src="https://i.imgur.com/auIkxAm.png" height="80%" width="80%" alt="Task 1"/>
</p>
<br />

And that brings us to the end of this project. This was a great learning experience for me as I got to experience firsthand the Microsoft Azure portal and environment, I learnt how to use Windows Powershell and finally learnt how to use a SIEM. <br/>
Thank you for reading my report on this project. <br/>
-rikosxay
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
