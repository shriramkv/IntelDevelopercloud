# IntelDevelopercloud
The easier guidelines to setup the Intel Developer Cloud is presented below: 
Step by Step Guidelines for setting up the IDC and to launch the Jupyter Notebook.

1.	Generate an ssh key using the command ssh-keygen in the power shell as an administrator. 

2.	Open the generated key file using notepad and copy the contents of the file.(C:\Users\<<username>>\.ssh is the path - file name is id_rsa.pub, use the command notepad id_rsa.pub) 

3.	Nextly login or register into the Developer Cloud and add the key under the profile section. https://scheduler.cloud.intel.com/

4.	Open .ssh folder and create a config file with the below commands:
Host myidc
Hostname idcbetabatch.eglb.intel.com
User uXXXXXX #← Request "scheduled access" at https://scheduler.cloud.intel.com/#/systems" to get your user identifier.
IdentityFile ~/.ssh/id_rsa
#ProxyCommand ncat --proxy YourProxy:XXXX %h %p --proxy-type socks5 %h %p  ## Uncomment if necessary
ServerAliveInterval 60
ServerAliveCountMax 10
StrictHostKeyChecking no 
UserKnownHostsFile=/dev/null

5.	On Powershell type ssh myidc to connect to your head node instance. This will enable you to be authenticated. 

6.	Next to connect to an interactive node type in the below command:
srun --pty bash
source /opt/intel/oneapi/setvars.sh
This will get the batch node activated! You will see this clearly in the powershell terminal. u***@idc-beta-batch-head-node would get changed to u***@idc-beta-batch-pvc-node
7.	Configure your shell using the command conda init bash

8.	Close the existing instance to make sure that the configuration changes reflect using the command exit
9.	You are taken back to the head node again, connect to the interactive node again by repeating Step6 again.

10.	To check the available environments type in the command conda env list

11.	Choose the environment of your choice by typing in conda activate env_name

12.	Get and check the allocated socket by using the below command:
echo $(ip a | grep -v -e "127.0.0.1" -e "inet6" | grep "inet" | awk {'print($2)}' | sed 's/\/.*//')

13.	Note down the last 2 digits of the ip address.

14.	To activate Jupyter Lab use the following command:
jupyter-lab --ip 10.10.10.X  (Where X is the last two digits that you observed before in Step13)

15.	Open a fresh Powershell Instance and type ssh myidc -L 8888:10.10.10.X:8888 (Where X is the last two digits that you observed before in Step13)

16.	Open a local browser and type the following in the address bar: http://localhost:8888/lab

17.	In the preceding screen you will be asked for a token. This can be found in the first powershell instance on the 6th last line.

For Video Tutorial Visit - https://youtu.be/PhzlMQ8-GE4 
Git Clone: git clone https://github.com/shriramkv/oneAPI_Essentials.git 
