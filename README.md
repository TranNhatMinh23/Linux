# Linux
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


