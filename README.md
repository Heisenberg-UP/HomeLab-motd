# HomeLab-motd

Repository contains customized bash scripts for the update-motd.d/ folder. These scripts will alter the message of the day a user sees when they log into their Ubuntu 22.04.4 LTS server or terminal screen.

![Screenshot 2024-02-21 at 11 05 59 AM](https://github.com/Heisenberg-UP/HomeLab-motd/assets/99283516/cdead9f4-4906-4883-921f-4492c5a9ff85)

**Contents**                


	README.md - Contains description of repository, image of message of the day, and notes about installation                

	LICENSE - GNU General Public License v3.0      

	scripts/:  
		
		00-header - Bash file that prints server name and distribution information      
		10-help-text - Bash file that prints important documentation links    
		50-custom-landscape - Bash file that mimics the landscape-sysinfo command on Ubuntu at a low level    
		97-overlay-services - Bash file that checks if services and are active or inactive and relays their status    
		98-updates-available - Bash file that checks if there are any updates available and how many of them are security updates    
 		99-reboot-required - Bash file sees if a system reboot is required    

**Installation**		

1. Clone the repository to your ~/ folder. We will change the permissions since root will be handling your motd when you login.
	```bash
	git clone https://github.com/Heisenberg-UP/HomeLab-motd
	cd HomeLab-motd/scripts/ && sudo chmod 755 * && sudo chown root:root *
	```
2. Make a copy of the original motd scripts provided by Ubuntu for safe keeping. We will change the permissions so the original scripts are no longer executable.
	```bash
	mkdir original-motd && chmod 700 original-motd/
	sudo cp /etc/update-motd.d/* ~/HomeLab-motd/scripts/original-motd/ && sudo chmod 644 ~/HomeLab-motd/scripts/original-motd/*
	sudo rm /etc/update-motd.d/*
	```
3. Symbolically link personalized scripts to the root motd folder.
	```bash
	cd /etc/update-motd.d/
	sudo ln -s ~/HomeLab-motd/scripts/00-header
	sudo ln -s ~/HomeLab-motd/scripts/10-help-text
	sudo ln -s ~/HomeLab-motd/scripts/50-custom-landscape
	sudo ln -s ~/HomeLab-motd/scripts/97-overlay-services
	sudo ln -s ~/HomeLab-motd/scripts/98-updates-available
	sudo ln -s ~/HomeLab-motd/scripts/99-reboot-required
	```
4. Edit the 00-header file to print your server name. Change HomeLab to whatever you want. Look for the line:
	```bash
	text="HomeLab" # Server name
	```
5. Edit the 97-overlay-services file to check and print the status of your services. To accomplish this you need to alter the variables to look up the services you are hosting or monitoring. You will also need to edit the echo commands to echo the correct service name and the correct service status. Below is an example of how the lines of code should look. You will need to edit every variable in this file.
	```bash
	SAMBA="$(sudo systemctl status smbd | awk '/Active:/ {print $2}')" # Find out service status
	samba=$(print_status $SAMBA)
	```
	```bash
	echo "\033[1;35m*\033[0m \033[1;32mSamba\033[0m:\t\t$samba" # Samba service
	```
6. Once you have personalized your files to print the correct server name and show your desired services, you can test it by logging in and out of the server or by running:
	```bash
	sudo run-parts /etc/update-motd.d/
	```		




**Disclaimer**	    
	
Please edit, destroy, delete, build upon, or whatever you like with this repository! However, be aware that I am a novice at linux and bash scripting. I will not be able to lend a helping hand with any high level issues. I am providing this repository because I think my motd is cool and I want other people to be able to use it if they would like.

