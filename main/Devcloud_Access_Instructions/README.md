> >>>>>

<img width="1000" alt="intel-fpga-devcloud" src="https://user-images.githubusercontent.com/56968566/68611681-86f05600-046f-11ea-8d12-f5259d60e7da.png">

<div align="center">
<strong>FPGA DESIGN DEVELOPMENT AND WORKLOADS FOR HARDWARE ACCELERATION</strong>
</div>
<div align="center">
 Develop programmable solutions and validate your workloads on leading FPGA hardware with tools optimized for Intel technology. Use this cloud solution in the classroom to support acceleration engineering curriculum. 
</div>


<div align="center">
  <h3>
    <a href="https://software.intel.com/en-us/devcloud/FPGA">
      Website
    </a>
    <span> | </span>
    <a href="https://github.com/intel/FPGA-Devcloud/tree/master/main/Devcloud_Access_Instructions#devcloud-access-instructions">
      Devcloud Access Instructions
    </a>
    <span> | </span>
    <a href="https://github.com/intel/FPGA-Devcloud/tree/master/main/QuickStartGuides#Contents">
      Quickstart Guides
    </a>
    <span> | </span>
    <!-- <a href="https://github.com/intel/FPGA-Devcloud/tree/master/main/FAQ#FAQ"> -->
    <!--   CLI -->
    <!-- </a> -->
    <!-- <span> | </span> -->
    <a href="https://github.com/intel/FPGA-Devcloud/tree/master/main/FAQ#faq">
      FAQ
    </a>
    <span> | </span>
    <a href="https://forums.intel.com/s/">
      Contact Us
    </a>
  </h3>
</div>


# Devcloud Access Instructions

[TOC]



[br/>

## 1.0 Introduction

Welcome to the FPGA Devcloud. This cloud is an Intel hosted cloud service with Intel Xeon processors and FPGA acceleration cards. The FPGA Cloud has a number of development tools installed including Acceleration Stack, and Quartus Prime Lite / Prime Pro development tools. The FPGA Cloud hosts high end FPGA accelerator cards to allow users to experiment with accelerated workloads running on FPGAs.

These instructions detail how to connect your Windows PC to the devcloud which runs Linux. If you are attempting connectivity from a Mac or Linux machine, we do not offer exact instructions, but you can use the ssh key and config file details described here with other ssh terminals.

When you signed up for the Intel Devcloud, you were presented with three different instances to sign-up for: IOTG, ONEAPI or FPGA. IOTG is a standalone setup with its own login. FPGA is a superset of the ONEAPI instance. At the time of this writing, ONEAPI has 225 nodes and FPGA has 12 nodes. With the FPGA instance you can run all of the features of the ONEAPI instance and gain access to an additional 12 machines that have FPGA PAC cards and associated tools.

This set of instructions superscedes the instructions on the OneAPI login instruction site. Once you download your devcloud access key, use these instructions. Also note that if you are inside a firewall (e.g., Intel's firewall for Intel employees), the instructions differ so pay close attention to the changes in the config file if you are accessing the FPGA devcloud from behind a firewall.

Perform steps through section 5.3 and you will be able to run various workflows found in our Quickstart guides. Information after this section is useful for topics such as batch flows (recommended), graphics, and job control.

**Note:** Please allow 60-90 mins to complete the entire setup. Also note the default account duration is 90 days. You will get reminders to renew your account if you need access for more than 90 days. If you allow your account to expire, you will lose the data in your account. We recommend copying source files back to your local machine for safe keeping.

## 2.0 Getting an Account

If you already have a Devcloud account, click [here](#connection-methods) to skip to the next step. 

**Please use this cloud website landing page to submit a request to access the FPGA Cloud:**

**https://intelsoftwaresites.secure.force.com/fpgadevcloud**

Once you've signed up, you should get an immidate screen response with your new user ID and instructions on how to set up your account. You will also receive a follow up email from Intel Devcloud which can take **1 hour** giving you a record of your user ID and your user ID key for login. This is an example of the resulting email which will be sent to you:

```
Welcome "user name",

We are excited that you chose Intel® FPGA Cloud.  Free access. No downloads. No installations. No maintenance. 

Your account should already be activated. Below are your credentials for your reference. 
Unique Access URL: https://devcloud.intel.com/fpga/?uuid=cd1d...

User ID: u12345
UUID Key: cd1d...

Access to Intel® FPGA DevCloud typically expires after 120 days. However, longer access times are granted based on user request. To extend this access, please email fpgauniversity@intel.com and give the extension time needed to complete your project.

Getting started with FPGA Cloud:
1. Access detailed instructions for environment setup: https://github.com/intel/FPGA-Devcloud/tree/master/main/Devcloud_Access_Instructions#devcloud-access-instructions
2. If you have technical questions or recommendations, please post them to our FPGA forum: https://forums.intel.com/s/topic/0TO0P000000MWKFWA4/application-acceleration-with-fpgas
3. If you have unresolved issues, email fpgauniversity@intel.com and give us a detailed description of your problem.
It's all about you and your code. We look forward to the innovations you'll create.

- Your friendly Intel DevCloud Team 
```

### Connection Methods

Once you have an account / email received you are ready to start the process to setup your account within the cloud. 

There are different methods of terminal connections. Listed below are a few options you can select in choosing which Terminal application tool you would like to use. This guide focuses on the recommended method 1.

1. [Windows with Mobaxterm (SSH client)](#30-access-from-your-pc-via-mobaxterm-or-from-linux-terminal) (recommended)
2. [Windows with Cygwin](https://devcloud.intel.com/datacenter/learn/connect-with-ssh-windows-cygwin/)
3. [Windows with PuTTy](https://devcloud.intel.com/datacenter/learn/connect-with-ssh-windows/)
4. Access through Jupyter Notebooks

## 3.0 Access from your PC via MobaXterm or from Linux Terminal

**MobaXterm** is an enhanced terminal for Windows with an X11 server, a tabbed SSH client and several other network tools for remote computing (VNC, RDP, telnet, rlogin). **MobaXterm** brings all the essential Unix commands to Windows desktop, in a single portable exe file which works out of the box and makes your Windows PC look like a UNIX environment.  Note that the X11 server with Mobaxterm runs slow, so we don't recommend its use. The X2Go section shows how to gain GUI access. 

### 3.1 Install MobaXterm

1. Download the MobaXterm free edition: https://mobaxterm.mobatek.net/download-home-edition.html Note: Get the **installer edition**, not the portable edition. (The installer edition will enable you to save login profiles.) . Download zipfile, extract it and click on the msi file to install Mobaxterm.

   ![mobaxterm_edition](https://user-images.githubusercontent.com/56968566/67715527-3fee6500-f987-11e9-8961-6c0a38163bfc.png)

### 3.2 Open Local Terminal 

1. Launch MobaXterm using the installer. You should see the following:

   <img src="https://user-images.githubusercontent.com/56968566/67715801-c5721500-f987-11e9-95e0-bdf9f76b7f43.png" alt="mobaxterm_window" width=80% />

2. Click: **"Start local terminal"**. Within this console you can see your local PC based files using standard Linux operating system commands (ls, cd, vi and etc.). 

3. Navigate around with ```cd``` (change directory) and ```ls``` (list) you will recognize your Windows folders and files accessible through a UNIX interface. To view your "C" drive in Windows, cd /drives/c . If you type ls and cd you can navigate the hierarchy that you see in Windows File Explorer. When your navigate to home through cd, you are at C:\Users\<username>\Documents\MobaXterm\home on your PC.

   Return to home by typing: ``` cd ```

   ![image](https://user-images.githubusercontent.com/56968566/69997123-4c2a8c80-1508-11ea-89d0-547a8a40515f.png)

### 3.3 Downloading an SSH key

To start the process:

1. Click on the following link to access the Connect website: https://devcloud.intel.com/fpga/connect/#.

2. Once you sign in, the following page will then be displayed. Click on the "SSH key for Linux/macOS/Cygwin" blue button under Step 3: Get SSH Key to download your key.

   ![image](https://user-images.githubusercontent.com/59750149/98843165-d1e8d480-2407-11eb-8ef2-79db18d04428.png)

5. Once you have downloaded the SSH key, return to these GitHub Instructions.

6. Create the directory ~/. ssh, unless it already exists and move the private SSH key into permanent storage in ~/.ssh:

   ```bash
   mkdir -p ~/.ssh
   mv /drives/c/Users/<user>/Downloads/devcloud-access-key-12345.txt ~/.ssh/
   ```

7. Add the following lines to files ~/.ssh/config:

   ```bash
   Host devcloud 
   #replace with your own user name
   User u12345
   IdentityFile ~/.ssh/devcloud-access-key-12345.txt
   ProxyCommand ssh -T -i ~/.ssh/devcloud-access-key-12345.txt guest@devcloud.intel.com
   ```

   If you saved your key in a location other than /drives/c/Users/<user>/Downloads, insert the correct path and the correct user number that was provided to you in the email. 

8. Set the correct restrictive permissions on the private SSH. Run the following commands in terminal: 

   ```bash
   chmod 600 ~/.ssh/devcloud-access-key-u12345.txt
   chmod 600 ~/.ssh/config
   ```

**The next steps to connect to the Intel Devcloud are different for usage inside and outside a firewall. Select the correct usage option below:** 

[Public User](#public-user---anyone-not-working-inside-firewall)\
[User Inside a Firewall](#user-inside-a-firewall)

## 4.0 Connection to Devcloud

### Public User - anyone not working inside a firewall

After the preparation steps above, you should be able to log in to your login node in the Intel Devcloud without a password. 

Enter the following: 

```
ssh devcloud
```

Upon the first login, you will be asked to add the host devcloud to the list of known hosts. Answer **yes**.

```bash
The authenticity of host 'devcloud' (<no hostip for proxy command>)' can't be established.
ECDSA key fingerprint is SHA256:...
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'devcloud' (ECDSA) to the list of known hosts.
# We are in!
logout
Connection to login-1 closed.
```

Next time you log in, you will only need to type ```ssh devcloud ```

Click [here](#50-Connecting-to-Servers-Running-FPGA-Development-Software) to skip to the next step. 

### User Inside a Firewall

You cannot log into the Intel Devcloud through the above steps if you are within a firewall. This section contains the tunneling commands and MobaXterm modifications needed to bypass the firewall to connect to the Devcloud. 

### 4.1 Add socat Package

1. Go to the packages icon and left-click.

   ![packages_icon](https://user-images.githubusercontent.com/56968566/67716101-6234b280-f988-11e9-972a-7c13370e1adc.png)

   Your next step you will see the MobApt package manager for MobaXterm:

   ![socat](https://user-images.githubusercontent.com/56968566/67716113-6b258400-f988-11e9-828a-83c74b051b91.png)

2. Install the **socat package**. This will take approximately 9 minutes to install.

### 4.2  Preparing Configuration file for users behind a firewall

1. Add additional entries into your config file: 

   ```
   Host colfax-intel-proxy
   User guest
   hostname cluster.colfaxresearch.com
   IdentityFile ~/.ssh/devcloud-access-key-12345.txt
   ProxyCommand socat STDIO SOCKS4:proxy-us.intel.com:%h:%p,socksport=1080
   
   Host colfax-intel-proxy-shell colfax-intel
   #replace with your own user name
   User u12345 
   hostname devcloud
   IdentityFile ~/.ssh/devcloud-access-key-12345.txt
   ProxyCommand ssh -T colfax-intel-proxy
   ```

2. At your local machine prompt type: 

   ```
   ssh colfax-intel
   ```

   You will now be logged in:

   <img src="https://user-images.githubusercontent.com/59750149/98844931-415fc380-240a-11eb-8cd9-0908a16f2bc8.png" alt="image" width=75% />

Note that the following response:

tty: standard input: Inappropriate ioctl for device\
X11 forwarding request failed on channel 0 

is expected behavior.

Note you can also connect outside of the firewall using ssh devcloud, but make sure your VPN is off. This will not work when at inside a firewalled facility (like Intel employees may have active) unless you connect to the outside network.

## 5.0 Connecting to Servers Running FPGA Development Software

### 5.1 Understanding available resources

You are now logged into machine called login-2 (headnode). You cannot run compute jobs here. You need to run compute jobs on a powerful compute node server. Note that if there is no activity when connected to Intel Devcloud for ten minutes your connection will be terminated. Simply ssh back in if that happens. Note for longer running jobs, run in the background with the Linux & option.

launch Mobaxterm (your PC) --> ssh devcloud (login-2) --> devcloud_login (interactive compute_node) or devcloud_login -b (batch processing on a compute node)

Some nodes can run Quartus, OpenCL emulation and compile and HLS emulation, simulation and compile. The node capacity grows with additional servers periodically added.

Some nodes can connect to machines with the above capabilities and also are directly connected to Arria 10 and Stratix 10 PAC cards.

There are a series of detailed Linux commands shown below should you want to know the intricate details of how to connect to available compute nodes.

1. [Login Script (5.2)](#52-login-script)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;5. [Batch Jobs Report Status (5.6)](#56-report-status-for-jobs-running-on-the-devcloud)
2. [Development Setup Tool (5.3)](#53-development-tool-access-and-setup)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;6. [Deleting Batch Jobs (5.7)](#57-deleting-jobs-on-the-devcloud)
3. [Submitting Batch Jobs (5.4)](#54-submitting-batch-jobs) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;7. [Querying Device Availability (5.8)](#58-querying-device-availability)
4. [Submitting Jobs for a Specified Walltime (5.5)](#55-submitting-jobs-for-a-specified-walltime)

### 5.2 Login Script

To facilitate connectivity without understanding some of the details on the Linux OS, we offer a script that simplifies connectivity called devcloudLoginToolSetup.sh located under /data/intel_fpga/devcloudLoginToolSetup.sh . Source the script in your ~/.bashrc by including these three lines inside the .bashrc:

```
if [ -f /data/intel_fpga/devcloudLoginToolSetup.sh ]; then
    source /data/intel_fpga/devcloudLoginToolSetup.sh
fi
```

Now you can run devcloud_login command tools_setup command and follow the Devcloud login script instructions to connect to the appropriate compute node. The picture below shows what the current script appears as. When you type the command “devcloud_login”, the following output is shown. It separates the available nodes and what machines are capable of running. This file also 

###### Figure 1: Login Script Running

![](LoginScriptGif.gif)

###### Figure 2: Arria10 Node Login Script Selection

<img src="https://user-images.githubusercontent.com/59750149/81036560-60c2d600-8e54-11ea-91c0-b48023b006f7.png" alt="ArriaLogin" width=60% /> 

###### Figure 3: Arria10 OneAPI Node Login Script Selection

<img src="https://user-images.githubusercontent.com/59750149/81036504-3244fb00-8e54-11ea-9d2f-979a4ed382cf.png" alt="ArriaOapiLogin" width=60% />

###### Figure 4: Stratix10 Node Login Script Selection

<img src="https://user-images.githubusercontent.com/59750149/81036445-ff9b0280-8e53-11ea-86f5-94ba4f096d73.png" alt="StratixLogin" width=60% /> 

###### Figure 5: Compilation Node Login Script Selection

<img src="https://user-images.githubusercontent.com/59750149/81036359-afbc3b80-8e53-11ea-8f71-a300b9845ade.png" alt="StratixLogin" width=60% />

###### Figure 6: Specific Node Login Script Selection

<img src="https://user-images.githubusercontent.com/59750149/81090112-183a0580-8eb2-11ea-9628-fbe39af59ffc.png" alt="LoginScript" width=53% />

<br/>

Once you select a node to start an interactive login, it will also output the command required to set up the x2go window. Just copy and paste into a new mobaxterm terminal. This is only required if you are running tools requiring a GUI. 

###### Figure 7: x2go Command

 <img src="https://user-images.githubusercontent.com/59750149/80255690-4b6ad200-8632-11ea-83ea-39df83ab5852.png" alt="x2go" width=77% />

<br/>

Other features to the Devcloud login script are the ability to display available nodes, [submit batch jobs](#54-submitting-batch-jobs) from the headnode as well as to speed the user's interaction when wanting to log into a compute node interactively.

Instead of answering "What are you trying to use the Devcloud for? ..." every time to start an interactive login to a compute node, you can type the following:

```
devcloud_login -I <argument options>
-----------------------------------Argument-Options-------------------------------------
A10PAC <development-stack version>
A10OAPI
S10PAC
CO
SNN <s00X-nXXX>
```

Type the following to simply view a list of the available nodes, to etheir specifically choose a compute node when submitting a batch job or to start an interactive login:

```
devcloud_login -l
```

For more information, try "devcloud_login --help" on a terminal that is logged into the FPGA devcloud.

<img src="https://user-images.githubusercontent.com/59750149/81611116-5f7f3500-938f-11ea-9f7c-dbf2eca902c4.png" alt="dev_help" width=90% />

### 5.3 Development Tool Access and Setup

From a terminal that is logged into a compute node, to get Quartus Access and Quartus Setup you can source the bash scripts manually however its highly recommended to use the **tools_setup** command. This command will guide you through query of what compile workload you want to run and setup environment variables and search paths.

Another feature to the tools-setup function is the ability to speed the user's interaction when wanting to source the environment variable settings for a tool when interactively logged into a compute node. Instead of answering "Which tool would you like to source? ..." every time, you can type the following:

```
tools_setup -t <argument option>
-----------------------------------Argument-Options-------------------------------------
QL <Version>
QS <Version>
QP <Version>
HLS <Quartus Edition> <Version>
A10DS
A10OAPI
S10DS
```

The above command can also be included in a batch script. Simply include the following two lines to be able to use the tools-setup function within your batch script. Then [submit a batch job](#54-submitting-batch-jobs).

```
source /data/intel_fpga/devcloudLoginToolSetup.sh
tools_setup -t <argument option>
```

For more information, try "tools_setup --help" on a terminal that is logged into the devcloud.

<img src="https://user-images.githubusercontent.com/59750149/81037113-7507d280-8e56-11ea-8145-b095b83e24e5.png" alt="image" width=95% />

### 5.4 Submitting Batch Jobs

This section provides information on how to submit batch jobs on the Devcloud when logged into the headnode machine (login-2), to be executed on a compute node. 

To submit a batch job using the [**login script**](#52-login-script) provided, use the following:\
Note, [walltime](#55-submitting-jobs-for-a-specified-walltime) is optional; use if batch job needs more than 6 hours. Maximum Walltime is 48 hours for machines running RTL AFU/OpenCL and 24 hours for machines running OneAPI.

```
devcloud_login -b <argument options> [<walltime=hh:mm:ss>] <job.sh>
-----------------------------------Argument-Options-------------------------------------
A10PAC <development-stack version> <job.sh>
A10OAPI <job.sh>
S10PAC <job.sh>
CO <job.sh>
SNN <s00X-nXXX> <job.sh>
```

<br/>

To launch a batch job without using the login script, you must first know the name of the compute node machine (sxxx-nxxx) you want to use.\
Type the following after knowing the compute node name:

```
qsub -q batch@v-qsvr-fpga -l nodes=<s00X-nXXX>:ppn=2 -d . <job.sh>   #for nodes with attached PAC cards

qsub -l nodes=<s00X-nXXX>:ppn=2 -d . <job.sh>    #for compute only nodes and oneAPI nodes
```

<br/>

When you submit your batch job, you will be prompted with a job ID for your submission. With this ID you are able to query for job [status](#56-report-status-for-jobs-running-on-the-devcloud) and/or [delete](#57-deleting-jobs-on-the-devcloud) the job if desired.\
Once the job is completed, two files will be generated; *.sh.**e**xxxxx and *.sh.**o**xxxxx (where xxxxx is the unique job ID). The .exxxxxx file is the error log, and the .oxxxxxx file is the terminal log where success or failure of the commands can be determined.

Example:

```bash
devcloud_login -b A10PAC 1.2 job.sh
				or
qsub -q batch@v-qsvr-fpga -l nodes=s001-n139:ppn=2 -d . job.sh
----------------------------------job.sh--------------------------------------------
  1 date
  2 hostname
  3 source ~/JOB_DEMO/HelpToolSetup.sh
  4 tools_setup -t QL 18.1
  5 which quartus
  6 cd unknown_directory
```

###### Figure 1: Error logfile obtained

![errorimage](https://user-images.githubusercontent.com/59750149/79778493-a8425180-82ed-11ea-9f3a-c29f5d7cf945.png)

###### Figure 2: Terminal logfile obtained

![outputimage](https://user-images.githubusercontent.com/59750149/79783143-0f173900-82f5-11ea-85d1-ce51ec62bd60.png)

### 5.5 Submitting Jobs for a Specified Walltime

A user will be logged off a node if they have been using it for longer than 6 hours. To submit a job with a specified walltime longer than 6 hours (for compilations longer than 6 hours) use one of the following commands.\

To submit a batch job with a specified walltime using the [**login script**](#52-login-script) provided, use the following:\
Note, you must be logged into the **headnode** machine (login-2).

```
devcloud_login -b <argument options> walltime=<hh:mm:ss> <job.sh>
-----------------------------------Argument-Options-------------------------------------
A10PAC <development-stack version> walltime=<hh:mm:ss> <job.sh>
A10OAPI walltime=<hh:mm:ss> <job.sh>
S10PAC walltime=<hh:mm:ss> <job.sh>
CO walltime=<hh:mm:ss> <job.sh>
SNN <s00X-nXXX> walltime=<hh:mm:ss> <job.sh>


devcloud_login -b S10PAC walltime=08:00:00 job.sh     #Example with Walltime of 8 hours
```

<br/>

To launch a batch job without using the login script, type the following after starting an **interactive login** into a specified node:

```
qsub -l walltime=<hh:mm:ss> <job.sh>


qsub -l walltime=12:00:00 walltime.sh		#example of a file to be executed
-------------------------------- walltime.sh --------------------------------------
# begin walltime.sh

sleep 11h		# sleep command equivalent to a quartus compilation file requiring 11 hours of compilation
# alternatively, sleep 11h would be quartus_sh commands (i.e. quartus_sh --flow main.v) 

echo job success > ~/Documents/walltime_log.txt		# exit sleep at 11:00:00, output "job success" to walltime_log.txt
```

### 5.6 Report Status for Jobs Running on the Devcloud

To report the status of your jobs running on the DevCloud using the [**login script**](#52-login-script) provided, type the following:

```
qstatus
```

<br/>

To report the status of your jobs running on the DevCloud without using the login script, type the following:

```
qstat -s batch@v-qsvr-fpga
```

<br/>

The result for both of the commands above will be of the following form:

```
v-qsvr-fpga.aidevcloud: 
Job ID                  Username    Queue    Jobname          SessID   NDS   TSK   Req'd Memory      Req'd Time    S     Elap Time
----------------------------------------------------------------------------------------------------------------------------------
2390.v-qsvr-fpga.aidev  u27224      batch    STDIN             27907     1      2       --            06:00:00     R      01:15:02
```

### 5.7 Deleting Jobs on the Devcloud

Jobs can be terminated with the following command when nodes are hanging with stalled jobs: 

```
qdel XXXX.v-qsvr-fpga.aidevcloud
```

Where XXXX is the unique Job ID.

Note, the qstat command mentioned in section 5.6 displays job ID finishing with .aidev however to kill the job usng qdel you need to append .aidevcloud .

<br/>

This is **not recommended**, but it is another technique to delete a job from the headnode if a node is hanging. Type the following and look for the qsub commands:

```
ps -auxw 
```

Free up the node with the following command: 

```
kill -9 <job-id>
```

### 5.8 Querying Device Availability

Should you want more details on available compute resources and query what is available, continue with the instructions below.

To query if free nodes are available run the below command on the login-2 server (headnode).

```
pbsnodes -s v-qsvr-fpga | grep -B 4 fpga 	   #lists all nodes that host PAC cards
pbsnodes -l free -s v-qsvr-fpga	    		   #lists all free nodes that host PAC cards
pbsnodes | grep -B 4 fpga_runtime 	   		   #lists all OneAPI nodes
```

You will get a listing of free and busy nodes that connect to PAC cards, or a listing of free and busy OneAPI nodes.

If there is a free node, when you execute the command below you will be logged into a new machine within a minute or so. If no machine is available, you will be placed in a queue.

To login to a specific machine in interactive mode ( -I ), execute the following command:\
Note, substitute *s00X-nXXX* with appropriate server numbers

```
qsub -q batch@v-qsvr-fpga -I -l nodes=<s00X-nXXX>:ppn=2   #for nodes with attached PAC cards

qsub -I -l nodes=<s00X-nXXX>:ppn=2    #for compute only nodes and oneAPI nodes
```

When launching the qsub command, you can request additional memory with the following command. Note: Each job takes 2 slots, so when you request 10G, it's actually 10G*2 = 20GB.

```
-l h_vmem=10G
```

Now you have a high power machine available for powerful computing jobs. You only have an **interactive**  console available, but with no graphics.\
Note: MobaXterm has multiple tabs and three possibilities of where to be logged in: 

- Local Machine, your PC (eg. llandis-MOBL)
- devcloud (eg. login-2 login server)
- compute server (eg. s001-n137)

Be cognizant of which Mobaxterm tab and machine you are typing in.

At this point you will want to run a PC based product called **X2Go client** that will allow you to have a Linux based GUI Intel Quartus and multiple terminal usage. 

## 6.0 Graphics Usage on the FPGA Devcloud

In order to run GUI based applications such as Quartus and Modelsim, you will need to download an application on your PC called X2Go. X2Go is the remedy for slow graphics response from Mobaxterm running X11 or VNC windowing systems.

To download X2Go, navigate to this link on your PC browser: https://wiki.x2go.org/doku.php/download:start

Grab the **MS Windows version** – click where the cursor is in the screenshot below <u>**(mswin)**</u>:

![launching_x2go](https://user-images.githubusercontent.com/56968566/67716221-a6c04e00-f988-11e9-97a6-bae636d8732b.png)

Go through the install steps for the mswin X2Go Client and accept all.

### 6.1 Opening Port for Graphics Usage in X2Go

Repoen the MobaXterm window, open a second session tab by clicking on the "+" as shown below:![image](https://user-images.githubusercontent.com/56968566/69987433-5b074400-14f4-11ea-9046-eb3d39ca0f69.png)

This tab will a launch terminal running UNIX commands on your local (PC) machine. You should have two tabs open. The first tab should be logged into login-2. The second tab will be logged in to your PC. Recall when you ran devcloud_login you see a message that needs to be pasted into the PC tab as described in the next section. **To open the port for graphics usage, use the devcloud_login function (sec 5.1) and copy and paste the appropriate ssh command shown as an output from this function into the tab that is logged into your PC**. 

Examples of this command are shown below based on inside and outside a firewall. 

```
ssh -L 4002:<s00X-nXXX>:22 devcloud			# Public User Example

ssh -L 4002:<s00X-nXXX>:22 colfax-intel		# Inside a Firewall Example
```

![image](https://user-images.githubusercontent.com/56968566/69987632-c7824300-14f4-11ea-84c7-682490dc19f8.png)

Launch the x2go application on your PC. Set up the new session with the following settings substituting the Login field </ uXXXXX /> with your own assigned user name and the path to the RSA/DSA key for ssh connection. This is the same key referenced for MobaXterm connection that enables ssh devcloud.

<img src="https://user-images.githubusercontent.com/56968566/70007979-1943c100-1527-11ea-8cc0-685a5b50cfcb.png" alt="image" width=60% />

The input/output screen has a setting for the display size which can be adjusted depending on your screen size. Adjust the parameters on this panel to change to a different screen size. To determine what DPI to use for your monitor, type the following command in a MobaXterm terminal: 

```
xdpyinfo | grep dot
```

<img src="https://user-images.githubusercontent.com/56968566/70003091-f8736f80-1516-11ea-9b36-666084afee51.png" alt="image" width=57% />


To launch the application, hit **OK** to save the settings and then click on the **New Session** icon to launch a graphics session.

<img src="https://user-images.githubusercontent.com/56968566/69988900-6871fd80-14f7-11ea-8af1-dddc9c0adaad.png" alt="image" width=77% />

After a minute or so, you should see the X2GO screen, be patient. While waiting for X2GO to launch you will see a screen that looks like this:

![image](https://user-images.githubusercontent.com/56968566/69988847-4c6e5c00-14f7-11ea-8804-6394099a3b85.png)

Click **Yes** when the following window pops up. 

![image](https://user-images.githubusercontent.com/56968566/70008081-5314c780-1527-11ea-8c47-ad27b69222d7.png)

You might get the following message if you previously logged into a different machine:

<img src="https://user-images.githubusercontent.com/56968566/67716812-b55b3500-f989-11e9-8c60-9c0eaaee2172.png" alt="host_key_verification_terminate" width=67% />

Enter **No**.

Then another dialog box will appear, enter **Yes**,

<img src="https://user-images.githubusercontent.com/56968566/67716830-bee49d00-f989-11e9-86b4-5aee8f792b5e.png" alt="host_key_verification_update" width=67% />

You will see a window that looks like the following. If a window opens up, click **Default**.

![x2go_desktop](https://user-images.githubusercontent.com/56968566/67716843-c60bab00-f989-11e9-9d99-2fbbdcfce6d9.png)

If X2GO fails to launch, check that you ran the tunneling command on Mobaxterm on your local host. Click [here](#6.1-Opening-Port-for-Graphics-Usage-in-X2Go) to be redirected to the section regarding this tunneling command. 

If you still aren't able to launch X2Go, temporarily disable your firewall (eg. McAfee) before launching a new X2Go graphics session.

In X2GO, right click within the desktop and select “Open Terminal Here”.

<img src="https://user-images.githubusercontent.com/56968566/67716892-dfacf280-f989-11e9-9d36-6e6c895c363e.png" alt="open_terminal" width=30% />

Your GUI ready environment should  be similar to the following image:![image](https://user-images.githubusercontent.com/56968566/69988693-ff8a8580-14f6-11ea-8b38-16ab19094b37.png)

To change the font sizing of the Desktop files in **Desktop Settings** under the **Icons** tab. Select “**Use custom font size**” and change it to 5 or to your font size preference.

<img src="https://user-images.githubusercontent.com/56968566/67716947-03703880-f98a-11e9-9b5f-e3b2b7eb79ad.png" alt="x2go_change_font" style="zoom: 80%;" />![x2go_fontsize](https://user-images.githubusercontent.com/56968566/67717026-27cc1500-f98a-11e9-9b01-f98c9a1a2d83.png)

<br/>

**<u>If you want to make the log-in experience shorter without the need of typing the lengthy qsub and ssh commands for future log-in, complete the following steps outlined here:</u>**

[Setup Devcloud Login Script Instructions](#52-login-script)

Note that X2Go is only available on nodes s001-n13[7-9] and s005-n005 at this time.

### 6.2 Quartus Font Setup

Note, for any GUI based activity you need X2Go running. Based on network activity GUI response could be considerably slower speed than when running on a local PC. Try to structure your project to use batch commands for faster response through the terminal.

If the Quartus font appears too zoomed in, as shown below, complete the following:

Under the Tools tab on the Main Bar, select Options. In the General Category, select “Fonts” and change the text size to 6.

<img src="https://user-images.githubusercontent.com/56968566/67717114-55b15980-f98a-11e9-857e-8c8f5d572d51.png" alt="quartus_options"/>

 ![quartus_fontsize](https://user-images.githubusercontent.com/56968566/67717117-5649f000-f98a-11e9-92fe-2864e3d9b155.png)

## 7.0 Transferring Files to and from the Devcloud 

**There are four different ways to Transfer Files to and from the Devcloud:**

1. [From/To a Local PC to/from DevCloud Server in X2Go Terminal (7.1)](#71-transferring-files-to-and-from-the-devcloud-with-scp)

2. [MobaXterm User Session (7.2)](#72-using-mobaxterm-to-transfer-files)

3. [WinSCP Application (7.3)](#73-using-winscp-to-transfer-files)

4. [MobaXterm Command Line to Transfer URLs (7.4)](#74-using-mobaxterm-command-line-to-transfer-urls-github) (recommended)

### 7.1 Transferring Files to and from the Devcloud with SCP 

**You can only use the local terminal on your PC to transfer files. Note: If on a firewall, replace devcloud with colfax-intel.**

Transferring Files from your localnode terminal. Your prompt on mobaxterm would be of the form: /home/mobaxterm (localnode)

```
scp /path/to/local/file devcloud:/path/to/remote/directory
```

From headnode or computenode to the localnode. 

```
scp devcloud:/path/to/remote/file /path/to/local/directory
```

Here is an example:

```
scp /drives/c/User/username/Documents/file.txt devcloud:/home/u12345
```

### 7.2 Using MobaXterm to Transfer Files

MobaXterm can be used to transfer files to and from your local PC to the Devcloud server.

<u>**To setup this feature, make sure that you have completed all the steps to connect to the DevCloud.**</u>

1. In the main toolbar of MobaXterm, click the **Session** button. ![mobaxterm_new_session](https://user-images.githubusercontent.com/56968566/67717144-65c93900-f98a-11e9-870b-784e76806a7f.png)

2. Select **SSH**. <img src="https://user-images.githubusercontent.com/56968566/67717168-6d88dd80-f98a-11e9-987a-3d226b109886.png" alt="mobaxterm_ssh" width=20% />

3. Enter the following information:
   1. Remote host: **localhost**
   2. Specify username: u12345 (edit to your username)
   3. Port: **4002**
      ![image](https://user-images.githubusercontent.com/56968566/69988244-1da3b600-14f6-11ea-8276-39ae5e70ef7d.png)

4. Under **Advanced SSH settings** > Select **Use Private Key** and search for the private key you used when you setup your DevCloud log-in. 

5. Click **OK**. 

6. If a new tab does not open, double-click on the side window **localhost (u#)**

   ![localhost_user_session](https://user-images.githubusercontent.com/56968566/67717217-82657100-f98a-11e9-8e15-30a98a73741e.png)
   
   The localhost user directory tool can be re-opened and closed as necessary to transfer files. Files can be transferred by dragging and dropping into the side-bar that displays the contents of the user saved in the DevCloud directory. 
   
   ![image](https://user-images.githubusercontent.com/56968566/69988329-52177200-14f6-11ea-8924-da19a9c5a236.png)

### 7.3 Using WinSCP to Transfer Files

To have WinSCP working, please have a tunnel open connected to X2GO. This should be done by having a new mobaxterm tab open and connecting to X2GO through an SSH tunnel to the node selected.

1. Download WinSCP: https://winscp.net/eng/download.php

   Click on the “Download WinSCP” Button and Install onto PC. Download with default setup: **Typical installation (recommended)** and **Commander User Interface Style**.

   ![winscp_download](https://user-images.githubusercontent.com/56968566/67717718-7ded8800-f98b-11e9-8bfa-ef0ea0d71070.png)

2. When you open WinSCP you should get a screen like this:

   ![winscp_open_window](https://user-images.githubusercontent.com/56968566/67717741-8a71e080-f98b-11e9-9ccb-ecc7ba91e9cf.png)

3. Click on the button “**Advanced…**”

   ![winscp_advanced](https://user-images.githubusercontent.com/56968566/67717752-8f369480-f98b-11e9-913e-965213997e4d.png)

4. Open the “**Authentication**” Tab under “**SSH**”

   ![authentication_ssh](https://user-images.githubusercontent.com/56968566/67717764-965da280-f98b-11e9-8623-3692b5509b8e.png)

5. Click on the **“…”** box top open a dialog box

   ![browse_for_sshkey](https://user-images.githubusercontent.com/56968566/67717776-9c538380-f98b-11e9-90a4-3cbf01043f88.png)

6. Navigate to where your Devcloud access key is located in the folder .ssh. Select the options box on the bottom right that says, “Putty Private Key Files” and switch it to “All Files”. Select your Devcloud key .txt file.

   ![putty_private_key_files](https://user-images.githubusercontent.com/56968566/67717790-a37a9180-f98b-11e9-8bed-4af4fbb5df50.png)

7. This new window should open asking if you would like to convert the SSH private key to PuTTY format. Press **OK** to this. Then press **Save** in the new window that opens. Then **OK** once more.

   ![convert-to-private-key](https://user-images.githubusercontent.com/56968566/67717841-bab97f00-f98b-11e9-8614-b2c897606bd5.png)

8. Press **OK** and return to the original screen.

   ![type-in-localhost-information](https://user-images.githubusercontent.com/56968566/67717855-be4d0600-f98b-11e9-97cc-ba3044551548.png)

9. Fill in the following information:

   Host name: Type in “localhost”\
   Port number: Type in 4002\
   User name: Type in the user name that was assigned to you

   ![image](https://user-images.githubusercontent.com/56968566/69988420-7a06d580-14f6-11ea-963d-40a465304dcb.png)

   Press **Save** to save all the information you just inputted for next time, and then press **OK**

   Press **Login**

Note: When re-using WinSCP to transfer files, re-open the application and **Login**. A new window will pop-up. Click **Update** and you should be able to access and transfer your Devcloud files on the server again. 

### 7.4 Using MobaXterm Command Line to Transfer URLs (Github)

You must be at the directory where you want to download the file from the Github site before running any of the two commands.

First copy the specific file's raw link from GitHub. (Open the file in Github, and on the top right corner click on 'Raw' to open the file in raw mode. Copy the URL).\
![image raw-link](https://user-images.githubusercontent.com/59750149/77709776-58d86200-6f89-11ea-89e5-10049dca22c1.png)

Then, use one of the following:

#### 1. WGET Command

**Wget** command retrieves content from web servers.\
Use the wget command in command line providing one or more URLs as arguments to download the file(-s). Note use wget -N to replace a file that already exists with the same name.

```bash
wget http://www.example.com/
```

![Image Wget](https://user-images.githubusercontent.com/59750149/77707156-8a4d2f80-6f81-11ea-982a-5bc970884e83.png)

#### 2. CURL Command

**Curl** command is used to copy a specific file from a public github repository, and it also allows you to rename the file as shown in the figure below.\
Use the curl command in command line to download the file.

```bash
curl -o filename http://raw.githubusercontent.com/example-file
```

![Image curl](https://user-images.githubusercontent.com/59750149/77707877-b36ebf80-6f83-11ea-8f6e-3f36c36d0e51.png)

<br/>

Note, when using any of the two commands above you may have added '/r' characters within your downloaded files. To removed this added characters use the following command: `tr -d '/r' < filename > newfilename`

## 8.0 Launching Development Tools

Quickstart Guides are available at the Quickstart Guide section of this git site https://github.com/intel/FPGA-Devcloud/tree/master/main/QuickStartGuides#Contents and are updated frequently.

## 9.0 Downloading an .sof to the Devcloud connected DE10-Lite Board

Node s001-n138 has a DE10-Lite development board connected to the USB port. Login to this machine and you will see a programmer connection USB Blaster 1-13 to the board. Note there is only one DE10-Lite on the network.![image](https://user-images.githubusercontent.com/56968566/69988508-a1f63900-14f6-11ea-8fd3-cfb688faedc7.png)

If the USB Blaster is not configured, complete the following steps: 

- [ ] To download your completed FPGA design into the local device, connect the USB Blaster cable between your PC USB port and the USB Blaster port on your development kit. If you are not using the DE10-Lite, you may have to plug the kit into power using a wall adapter. Upon plugging in your device, you should see flashing LEDs and 7-segment displays counting in hexadecimal, or other lit up LEDs and 7-segments depending on previous projects that have been downloaded to the development kit. 

***Note: The lights and switches controlled on the Devcloud connected server kit cannot be controlled unless system console or another form of instrumentation is used.***

- [ ] To use the USB Blaster to program your device, you need to install the USB Blaster driver. To begin, open your Device Manager by hitting the Windows Key and typing Device Manager. Click the appropriate tile labeled Device Manager that appears.

- [ ] Navigate to the Other Devices section of the Device Manager and expand the section below. 

  ![device_manager](https://user-images.githubusercontent.com/56968566/67718301-be99d100-f98c-11e9-8e24-a04edfa7f1ea.png)

- [ ] Right click the USB Blaster device and select **Update Driver Software**.

- [ ] Choose to browse your computer for driver software and navigate to the path shown below.

  ![browse_driver_software](https://user-images.githubusercontent.com/56968566/67718364-da9d7280-f98c-11e9-9677-ed7d9a3a39b9.png)

- [ ] Click on **Next** and the driver for the USB Blaster should be installed.

## 10.0 Compiling on the Devcloud and Downloading to a Local PC connected DE10-Lite board

[10.1 Setting up USB Tunneling from Devcloud to Local PC USB Blaster](#101-setting-up-usb-tunneling-from-devcloud-to-local-pc-usb-blaster)

[10.2 Programming a Design from the Devcloud to a Local PC Connected FPGA](#102-programming-a-design-from-the-devcloud-to-a-local-pc-connected-fpga)

### 10.1 Setting up USB Tunneling from Devcloud to Local PC USB Blaster

- [ ] On your PC, launch the Quartus Programmer. Search **Programmer** in the File Explorer. 

  <img src="https://user-images.githubusercontent.com/56968566/67718453-01f43f80-f98d-11e9-9745-3f596993ced4.png" alt="programmer" width=67% />

- [ ] If you don’t have the Programmer on your PC, download it from this link: http://fpgasoftware.intel.com/18.1/?edition=lite&download_manager=dlm3&platform=windows

- [ ] Select **Additional Software** and download the **Quartus Prime Programmer** and **Tools**.

  ![download_programmer_intel](https://user-images.githubusercontent.com/56968566/67718603-55ff2400-f98d-11e9-9343-0e499609f487.png) 

- [ ] Follow the login prompts, download, and install the Programmer. 

- [ ] For usage within the Firewall, in the File Explorer Search window, search ''**Programmer**'', and select **Run as administrator**. For other users, you can open the Programmer (Quartus Prime 18.1) normally. 

  <img src="https://user-images.githubusercontent.com/56968566/67718645-64e5d680-f98d-11e9-9987-ea2d1ea6344c.png" alt="programmer" width=77% />

- [ ] Select **Yes** if a yellow window will pop-up asking if you to allow app changes from an unknown publisher. 

- [ ] The Programmer window should then pop-up.  

- [ ] Left click on **Hardware Setup…** and then select the **JTAG Settings** tab.

  <img src="https://user-images.githubusercontent.com/56968566/67718852-dde52e00-f98d-11e9-9c06-39ac5c61aa5d.png" alt="download_programmer" width=57% /><img src="https://user-images.githubusercontent.com/56968566/67718870-eccbe080-f98d-11e9-83b8-1a7738f3f018.png" alt="run_admin" width=57% />

- [ ] Click on **Configure Local JTAG Server...**

- [ ] **Enable remote clients to connect to the local JTAG** server and **enter a password** in the prompt box and **<u>remember this password</u>**. It will be used to connect later.

  <img src="https://user-images.githubusercontent.com/56968566/67718930-0f5df980-f98e-11e9-92ce-21c5476c11b2.png" alt="hardware_setup" width=47% />

- [ ] On your local PC terminal, type in the following command to tunnel from the DevCloud to your local USB: **Note: the last parameter points to the node 138. For server consistency, you need to adjust this to the node number you are currently using to connect to the Devcloud.**

  ```
  ssh -tR 13090:localhost:1309 colfax-intel "ssh -t -R 13090:localhost:13090 s001-n138"
  ```

- [ ] Ignore the messages: 

  ```
  stty: standard input: Inappropriate ioctl for device
  X11 forwarding request failed on channel 0
  ```

- [ ] On the X2Go app and Quartus Prime Lite window, launch the programmer by selecting **Tools** > **Programmer**. 

  <img src="https://user-images.githubusercontent.com/56968566/67718964-20a70600-f98e-11e9-99ac-d897ffa295cd.png" alt="configure_JTAG" width=70% />

- [ ] Left click on **Hardware Setup,** select the **JTAG Settings** tab, and **Add Server**.

  <img src="https://user-images.githubusercontent.com/56968566/67718986-2a306e00-f98e-11e9-9d06-24ccc2173801.png" alt="JTAG_password" width=67% />

- [ ] Enter in the following information: 

  Server name: **localhost:13090**\
  Server password: (password you set up for your PC local JTAG server)

- [ ] Select **OK**, and you should see the localhost on the list of JTAG servers.

  <img src="https://user-images.githubusercontent.com/56968566/67719028-3d433e00-f98e-11e9-8c3d-fcaf6cec4aba.png" alt="add_server_JTAG" width=67% />

- [ ] Click on the **Hardware settings tab,** double click on the **localhost:13090**, and that should now be your selected USB blaster download connection. 

- [ ] Make sure localhost:13090 shows up as your currently selected hardware and that the connection status is OK.

### 10.2 Programming a Design from the Devcloud to a Local PC Connected FPGA

- [ ] Select the .sof file to be downloaded to the FPGA. 

- [ ] Click **OK** and click **Start**. The progress bar should show 100% (Successful) and turn green. If it fails the first time, click **Start** a second time. 

  ![100_succesful](https://user-images.githubusercontent.com/56968566/67719042-446a4c00-f98e-11e9-994f-2bcb55469fd0.png)

## 11.0 Timeouts and Disk Space

Your session will timeout after six hours after login. Batch submissions must complete within 24 hours or the job will terminated. Each user has access to 200 GB of disk space on the Devcloud.

If you find that you are kicked off the Devcloud due to short bursts of inactivity, this can be attributed to your PC display going to sleep. Complete the following steps to avoid session time-out:

1. In the Windows search bar, search "**Display settings**." 
2. Select in the side-bar **Power & Sleep**. 
3. Under **Screen**, change both settings to **Never**. 

## 12.0 Determining and Allocating Memory Availability and CPU Count and Speed

Enter the following in a Devcloud Terminal to determine memory availability: 

```
dmesg | grep Memory:
```

Enter the following in a Devcloud Terminal to determine CPU Count and Speed:

```
lscpu
```

When launching the qsub command, you can request additional memory: 
Note: Each job takes 2 slots, so when you request 10G, it's actually 10G*2 = 20GB.

```
-l h_vmem=10G
```


## 13.0 Devcloud Text Editors 

There are three available editors in the Devcloud terminal: 

1. [Gedit](https://help.gnome.org/users/gedit/stable/)
2. [Vi](https://www.washington.edu/computing/unix/vi.html)
3. [Emacs](https://www.digitalocean.com/community/tutorials/how-to-use-the-emacs-editor-in-linux)

For tutorials on how to use the editors listed above, click the hyperlinks to be redirected to a quick read tutorial site. 

## 14.0 Determining which machine and version of the OS is running on a Node

```
cat /sys/devices/virtual/dmi/id/product_name
cat /etc/os-release
```



## 15.0 Security

The devcloud accounts cannot be viewed from one user to another. There is no way of associating a login u numbers to a user name or organization. Users cannot change their protections so that other users can see their files. There are no group settings that open up that visibility. No user has sudo access, only the system adminstrator who works for a third party cloud service provider, Colfax International, has root access.

The PAC cards offer a security "sign" feature that associates a key with a bit stream. It is possible for users to sign their green bit stream or aocx file prior to programming the board.

Further details can be found in the license agreement:

https://devcloud.intel.com/datacenter/static/docs/terms/Intel-DevCloud-Access-and-Software-License-Agreement.pdf

https://devcloud.intel.com/datacenter/static/docs/terms/Colfax_Cloud_Service_Terms_v1.3.pdf



## 16.0 Jupyter Notebook Access

Some OneAPI labs run through a Jupyter notebook. To access, you need to reference your welcome email. You will see a line in the email of the form:

 in

Please find the instructions to access the DevCloud at:

https://access.colfaxresearch.com/?uuid=2953c785-0de5-40bd-8edh-86d6a70ab6ff

Access this web page: https://devcloud.intel.com/oneapi/get_started/

In the top of this web page you are asked to enter your uuid, and enter everything after the = symbol in your welcome email. Once logged in, follow the instructions on the Jupyter OneAPI web page.

## 17.0 Debug Notes - Tips and Tricks

Don't forget to check the Intel Forum(s), your issue and solution might be documented there:\
https://forums.intel.com/s/topic/0TO0P000000MWKFWA4/application-acceleration-with-fpgas?language=en_US

If you are not are not able to gain access to a compute node, because of this error: qsub: submit error (Unauthorized Request MSG=group ACL is not satisfied: user u#####@login-2, queue batch) it could be that you did not request access to the FPGA devcloud, and are in fact on the OneAPI devcloud. The FPGA devcloud is a superset of the OneAPI devcloud, and enables more machines connected to PAC cards. To check, type groups from login-2 node. If you do not see c009-fpga group, you are not in the right access group for the devcloud. Go to this site https://software.intel.com/en-us/devcloud/FPGA and click on the signup page. Sign up, and state you already have an account and want to be added to the c009-fpga group. State the u##### account number you were assigned.

------

<a href="#top">Back to top</a>

