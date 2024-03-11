# Hand-on Exercise on File Manipulation and User Permission with LinuxOS.
#Resource for this Exercise include:
#1. PC with Linux Os Installed as VM #2.Linux Distro: ubuntu20.04-LTS
#Virtual Machine is configured to use vagrant shell

#WORK FLOW
#1.Your login name: altschool i.e., home directory /home/altschool.
sudo useradd-m Altschool -
#(Creates a New User called Altschool with home directory)
sudo passwd Altschool:
#(To generate new password for User Altschool)
#New Password : (Prompts for passward)
#Retype New Password
#2.The home directory contains the following sub-directories:
code, tests, personal, misc
#Unless otherwise specified, you are running commands cdfrom the home directory.
su Altschool:
#(Login into the Shell of new User created)
echo $HOME
#(takes you to home directory of user newly created)
bash
whoami
#--(any of thr above to confirm the shell of the current user)
sudo mkdir code tests personal misc.
#(creates subdirectories from Home of of User - Altschool)
#3.Change directory to the tests directory using absolute pathname
cd /home/ALtschool/tests - (Ablsute path navigation)
#4.Change directory to the tests directory using relative pathname
cd ..
#(Backward navigation to parent directory
cd ./tests -
#(Relative path nagivation into child directory)
#5. Use echo command to create a file named fileA with text content ‘Hello A’ in the misc directory
echo &#39;Hello A&#39; &gt; /home/Altschool/misc/FileA
cat /home/Altschool/misc/FileA
#(View the read only format of file just created)

#6. .Create an empty file named fileB in the misc directory. Populate the file with a dummy content
afterwards.
touch /home/Altschool/misc/fileB -
vim /home/ALtschool/misc/FileB
#(above to populate file content with dummy content)
#7. Copy contents of fileA into fileC
cp /home/Altschool/misc/FileA /home/Altschool/misc/fileC
cat /home/Altschool/misc/fileC
#(Above to view content of fileC to confirm)
#8. Move contents of fileB into fileD
mv FileB FileD
#(above Move files B content into B and replace)
#9..Create a tar archive called misc.tar for the contents of misc directory
ls -l (list content of misc directory)
cd .. (change to the parent directory - Altschool)
tar -cvf misc-tar misc
#(above to creat a tar archive file ready for).
#10. Compress the tar archive to create a misc.tar.gz file
gzip misc.tar
#11.Create a user and force the user to change his/her password upon login.
sudo usermod -aG sudo Altschool
#(add altschool to sudoers to posses administrative privileges to you create a user) - (This command is ran
from the root user. chang to root- vangrant home to run this command- ensure your CLI prompt is blinking
&#39;#&#39; and not &#39;$&#39;)
su Altschool
#(change to user Altschool)
sudo useradd Kenny
#(above creates an new user)
sudo passwd --expire Kenny
#(expires password for User Kenny and will prompted to enter new password at login attempt).
#12. Lock a user&#39;s password
sudo passwd -l OR --lock User
#(lock user kenny password NOTE)
chage --list Kenny
#(defines paswd parameters)

sudo cat /etc/shadow
#(check status of locked paswd. exclamation mark (!) shows that it is locked)
sudo passwd -u Kenny
# (unlocks user password)
#13. Create a user with no login shell
sudo useradd -s /sbin/nologin Adaga.
#ALTERNATIVLY:
sudo adduser Favour --system
#(another method of creating a nologin user with Home directory)
tail /etc/passwd | grep nologin
#(to view the status of the no login user created on read-only format)
#Alternatively
sudo vi /etc/passwd (if the user already exist and want to put apply a nologin restrictions )
type &#39;I&#39;
#for insert mode (without the type and open and close quote mark - to go to the user line and type(
/sbin/nologin)
type &#39;: set nu&#39;
#without the type and open and close quote mark - to set line number, if your using the Vim text editor
#14. Disable password based authentication for ssh
sudo vi /etc/ssh/sshd_config
#type &#39;i&#39; to chnage to INSERT MODE
# :set nu (to set line number - use up, down, left, right arrow keys to locate configuration information
setting
[&#39;PERMITROOTLOGIN&#39;]
#and edit by enabling or disable as you type &#39;Yes&#39;, or &#39;No&#39; to the queries)~ Remember to comment out your
edits by removing the &#39;#&#39; preceeding the configuration setting queries
press escape, and type :q ENTER
#to Save and return to command mode I&#39;d your editing with Vim text editor.
#15. Disable root login for ssh
sudo vi /etc/passwd
#(edit root log in , changing it to bin bash - /root:/bin/bash)
sudo service sshd restart
#-(to effect the changes)
#log in afterward with (vagrant ssh) to confirm if your settings have been effected or Not
