# Linux
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Automating Linux Administrative tasks
sudo apt update ̃̃&& sudo apt install ansible
ansible --version
id
cat servers.txt
ssh -l student -p 22 {{ipaddress}}
{{password}}
apt list --upgradable 
exit
ssh -l student -p 22 {{ipaddress}}
logout
vim hosts
[servers]
vps1 ansible_host=ip ansible_user=student
ansible -i ./hosts --list-hosts -all
sudo apt install sshpass // to use ssh with password phai install sshpass
sudo vim /ect/ansible/ansible.cfg // unenabled Host Key checking 
ansible -i ./hosts vps1 -m ping -u student -k //-m ping kiem tra ket noi SSH; -k mat khau; -u student is the username that will connect
ansible -i ./hosts all -m ping -u student -k
ansible -i ./hosts servers -m ping -u student -k
ansible -i ./hosts servers -m setup -u student -k

vim hosts
[servers:vars]
ansible_user=student
ansible_ssh_pass=Tuyenoccho
ansible_port=
cat 
ansible -i ./hosts servers -m setup
ansible -i ./hosts servers -m ping
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~Ansible ad-hoc command~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ansible -i ./hosts servers -m shell -a "df -h" -u student -k 
ansible de chay nhieu task dong; servers la name cua group se ket; -m entire group
ansible -i ./hosts servers -m shell -a "df -h" -f 10
ansible co 5 thread chay dong thoi -f de tang so luong thread 
ansible -i ./hosts servers -m shell -a "lsmem"
biet so Ram dang su dung
ansible -i ./hosts servers -m shell -a "free -m"
biet kha nang luu tru dang free 
ansible -i ./hosts servers -m shell -a "tail -n 3/etc/passwd"
Biet 3 nguoi chinh sua passwd cuoi
ansible -i ./hosts servers -m shell -a "ip address show def eth0"
Mac address
ansible -i ./hosts servers -m shell -a "ip address show def eth0" | grep ether | cut -d' ' -f6"
Chay la biet
ansible -i ./hosts servers -m shell -a "ip address show def eth0" | grep ether | cut -d' ' -f6" | grep -v ">>"
chiu
vim backup.sh
#!/bin/bash
tar -cfz /root/etc-$(date +%F).tar.gz /etc 
ansible -i ./hosts servers -m script -a "./backup.sh" --become -K
--become mean  run the script on the remote host as root or become root
ssh -l student ip
sudo ls /root/
exit
vim hosts
ansible_become_pass=ansible123-
Giup chay may remote ko can mat khau
ansible -i ./hosts servers -m script -a "./backup.sh" --become

~~~~~
chuot phai + split ho
cat hosts
ssh student@ip
yes
nmap -p 80 -sV scanme.nmap.org
ansible -i hosts servers -m apt -a "name=nmap state=present update_cache=true" -u student -k --become -K
ansible -i hosts servers -m apt -a "name=nmap state=absent purge=yes update_cache=true" --become

ansible -i ./hosts servers -m apt -a "name=nginx state=persent update_cache=true" --become
ansible -i ./hosts servers -m service -a "name=nginx state=started" --become
systemctl status 
ansible -i ./hosts servers -m service -a "name=nginx state=restarted" --become
ansible -i ./hosts servers -m service -a "name=nginx state=stopped" --become
ansible -i ./hosts servers -m service -a "name=nginx enabled=yes" --become
systemctl is-enabled nginx
~~~~~~~~~~~~~~~
ansible -i ./hosts servers -m group -a "name=developers state=present" --become
tail -n 3 /etc/group
tạo group và hiện 3 group mới nhất được tạo
ansible -i ./hosts servers -m group -a "name=developers state=absent" --become
tail -n 3 /etc/group
Xóa 
ansible -i ./hosts servers -m user -a "name=john state=present groups=developers create_home=yes comment=\"new user\"" --become
tail -n 3 /etc/passwd
ansible -i ./hosts servers -m user -a "name=john state=absent" --become
tail -n 3 /etc/passwd

ansible -i ./hosts servers -m user -a "name=john state=present groups=developers create_home=yes comment=\"new user\" shell=/bin/bas generate_ssh_key=yes ssh_key_bits=2048" --become
~~~~~~~~~~~~~cron
pgrep -l cron 
which crontab
ls -l /etc/crontab
crontab -l
crontab -e
##########################
## Task Scheduling using Cron
##########################
 
# editing the current user’s crontab file 
crontab -e
 
# listing the current user’s crontab file 
crontab -l
 
# removing the current user’s crontab file 
crontab -r
 
## COMMON EXAMPLES ##
# run every minute
* * * * * /path_to_task_to_run.sh
 
# run every hour at minute 15
15 * * * * /path_to_task_to_run.sh
 
# run every day at 6:30 PM
30 18 * * * /path_to_task_to_run.sh
 
# run every Monday at 10:03 PM
3 22 * * 1 /path_to_task_to_run.sh
 
# run on the 1st of every Month at 6:10 AM
10 6 1 * * /path_to_task_to_run.sh
 
# run every hour at minute 1, 20 and 35
1,20,35 * * * * /path_to_task_to_run.sh
 
# run every two hour at minute 10
10 */2 * * * /path_to_task_to_run.sh
 
# run once a year on the 1st of January at midnight
@yearly     /path_to_task_to_run.sh
 
# run once a month at midnight on the first day of the month
@monthly    /path_to_task_to_run.sh
 
# run once a week at midnight on Sunday
@weekly      /path_to_task_to_run.sh
 
# once an hour at the beginning of the hour
@hourly     /path_to_task_to_run.sh
 
# run at boot time
@reboot     /path_to_task_to_run.sh
 
All scripts in following directories will run as root at that interval:
/etc/cron.hourly
/etc/cron.daily  
/etc/cron.hourly  
/etc/cron.monthly
/etc/cron.weekly
~~~~~~~~~~~


