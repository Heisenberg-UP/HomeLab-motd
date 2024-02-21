# personalized-motd

Repository contains customized bash scripts for the update-motd.d/ folder. These scripts will alter the message of the day a user sees when they log into their Ubuntu 22.04.4 LTS server or terminal screen.

![Screenshot 2024-02-21 at 11 05 59 AM](https://github.com/Heisenberg-UP/personalized-motd/assets/99283516/cdead9f4-4906-4883-921f-4492c5a9ff85)

**Contents**                
                
README.md - Contains description of repository, image of message of the day, and notes about installation                
LICENSE - GNU General Public License v3.0    
scripts/    
        00-header - Bash file that prints server name and distribution information      
        10-help-text - Bash file that prints important documentation links    
        50-custom-landscape - Bash file that mimics the landscape-sysinfo command on Ubuntu at a low level    
        97-overlay-services - Bash file that checks if services and are active or inactive and relays their status    
        98-updates-available - Bash file that checks if there are any updates available and how many of them are security updates    
        99-reboot-required - Bash file sees if a system reboot is required    

