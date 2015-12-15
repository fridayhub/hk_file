# Installing the RCS Masternode, console and networking injector.

In this part we will be installing the complete Galileo RCS MasterNode.

## Disclaimer

I am not responsible for any actions you may take while using this software. You should already have knowledge about computers and you should know what you are doing. Educational purposes only.

So please don't run it on your physical machine lol.

## Credits and Shoutouts.

I have to credit [4Armed](https://www.4armed.com/) for their introduction on installing RCS. It caught my attention but they skipped lots of steps so no one could install the masternode.

Secondly I will shoutout to my boy [@4sterea](https://twitter.com/4sterea) with his [Captio.CH](http://captio.ch/) services. He's also the one who managed to install the Tactical Network Injector

## Just something I want to write.

I was really interested into installing the software. I managed to do so but lost interests and this project kind of died. Then I received some message from a kid who attempted to be a hacker(he really wasn't lol). He tried selling me an install. Then I decided to release this as I do not want people selling this.

And sorry for some of the grammar/spelling mistakes. English is not my native language.

## Requirements

You require the following things to get started:

* A pc that can run multiple windows vm's.
* A windows copy - In their documentation they say that you require server 2008 sp1 but windows home basic works just fine.
* The following files inside [this](http://hacked.thecthulhu.com/HT/FAE%20DiskStation/2.%20DELIVERY/2.3.%20Software%20%28releases%29/RCS%209.6%20%28stable%29/Product/Server/) directory. Do not download them now but you will want to save this link for later. You'll also require the Adobe AiR runtime later on.
* A virtualization program such as virtualbox or VMWare player/workstation. I used VMWare Workstation in this case so things might be different.
* Don't be a retard/someone who doesn't know what's going on. Yeah
* Minimal programming skill would be useful but since I will be providing all files it won't be necessary. 
* The files provided by me in this gist.
* [This legit license file](http://hacked.thecthulhu.com/HT/FAE%20DiskStation/4.%20INTERNAL/4.1.%20Product%20Licenses/RCS%209.6.x/LICENSE-MASTER-101866151-v9.6.lic)

## Alright lets start.

First off you want to start a new windows vm. I used windows home basic for this although it is recommended by HT that you use Windows Server 2008 SP1.

After you set your VM up you need to download both files that I linked in the requirements. You also want to save the files I post in this gist somewhere on the desktop. The last file you need to download is the license file which I also linked.

Now you want to open the rcs-setup file you just downloaded. Here are some of the settings you will require:

| Key      		| Value         			|
| ------------- |:-------------------------:|
| Install       | Master node   			|
| Admin pass    | GalileoRCS1   			|
| CN            | 127.0.0.1 				|
| License       | rcs-license-patched.lic   |

That should now begin installing rcs. Credits to 4Armed for figuring out the license bypass for installing.

Alright so now you want to open the folder where you keep the rcs-license-check-patched.rb and copy all the contents of the file to your clipboard.
Open an explorer to **C:\RCS** and wait until the installer says something along the lines of "*Removing previous master node files*". 

When that happens quickly navigate to **C:\RCS\DB\bin** and look for the **rcs-license-check** file. It might not appear instantly but when you see it open it up and replace the contents with your clipboard contents.
The installer should now verify the license with success. When done navigate to **C:\RCS\DB\config** and replace the rcs.lic file with the legit license which is linked in the requirements.
Now it's just waiting. **The installing cores step may take up to 20 minutes so do not think that it has crashed.**

When done open up a console and execute the following commands:

```
cd C:\RCS\DB\bin
rcs-db-config -n LOCAL/WANIP -g
```
This should now allow you to connect with success later.

After configuring rcs-db it will still tell you that there's no dongle inserted. It will log this in the rcs logs. I have provided a bypass file for that so open up **dongle-patched.rb** and copy the contents.
Navigate to the **C:\RCS\DB\lib\rcs-db-release** directory and open up dongle.rb and replace the contents of the file with the dongle-patched.rb contents you copied onto your clipboard.

Restart the vm and check the rcs-db log inside **C:\RCS\DB\log**. It should say "*Dongle Bypass Coded by Looka @ HF*" somewhere in the log and should also have no errors with the db connection.

## Installing the console

I recommend installing the rcs-console on the same machine as the rcs-master node. Download the adobe air installer and install it. Now navigate to **C:\RCS\DB\console** and install the rcs-console package.

Once opened enter the following information:
* Username: admin
* Password: GalileoRCS1
* Server: 127.0.0.1

You should now be able to login with success. It will ask you about an ssl certificate but select yes. You are now inside the rcs-console.

## Installing the networking injector and configuring it with master node.

It's rather easy to install the network injector. This tool is used at locations where they want to intercept network. It's kind of like a huge MITM tool.

### Requirements:

You require one more file for this to function which is the [Network injector iso](http://hacked.thecthulhu.com/HT/FAE%20DiskStation/2.%20DELIVERY/2.3.%20Software%20%28releases%29/RCS%209.6%20%28stable%29/Product/Injector/networkinjector-9.6.0.iso).

Create a new VM with this iso and boot it up. Once created select the option "Install Tactical Device". This process may take some time so get a cup of tea or whatever.
When it requires a pass phrase enter the phrase "firstboot". Credits to [@4sterea](https://twitter.com/4sterea) from [Captio.CH](http://captio.ch) for this pass phrase.

Now it will ask you to setup an user. I used the username "ht" and password "ht" for this testing purpose(Also next time you boot up use the password you set for this user as pass phrase).
After the install open the "Tactical Control Center" app inside your just created vm. Then go to your RCS Console and go to System -> Network Injectors. Create a new injector called Injector1 and export the key. Put the key somewhere where the network injector vm can get it.
In System Management import that zip as key in "System Management" and enter the master node ip and port 4499(Somehow that worked for me), finally you want to hit configure.

You now installed the networking injector. We can use Network Inject but you can also use Wireless Intruder, Fake Access Point, Physical Unlock and more features. 

## That was it for now, check out these following things

So yeah that was the release for now.

I recommend you read the following items found [here](http://hacked.thecthulhu.com/HT/FAE%20DiskStation/2.%20DELIVERY/2.3.%20Software%20%28releases%29/RCS%209.6%20%28stable%29/Documentation/EN/)

You will also enjoy 4Armed's guide as they will teach you how to setup an actual agent.




