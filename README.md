# App-Listing

## Description
 This program is used to list out the applications installed on computers running Windows OS and present in the same network. It uses Secure Socket Shell (SSH) and Secure File Transfer Protocol (SFTP) to connect and obtain applications installed details from a remote system. SFTP is used to transfer the script which runs in the remote machine and obtains the information. In this program, two scripts are used which are “ssh multiple.py” and “app_list.exe”.
“app_list.exe” is the main script. It uses the winapps python library, which manages and shows all the application information of the remote machine. This script is present only on the host machine and is transferred to the remote machine through the SFTP protocol.
“ssh multiple.py” is used to establish connection and transfer the script to the remote machine. “ssh_ip.csv” is used as the input file, to input the ip addresses of the remote machines. The data obtained is stored in a csv file named “outfile.csv” on the host machine
# code
```
import paramiko
import csv
with open('ssh_ip.csv') as input_file:
     ip_reader = csv.reader(input_file, delimiter=' ')
     for row in ip_reader:
        ip = row[0]
        print(ip)

        client = paramiko.SSHClient()
        client.load_system_host_keys()
        client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
        client.connect('{}'.format(ip), username='snehs', password='Alpha@echo01')

        sftp = client.open_sftp()
        sftp.put(r'D:\apps.exe', 'C:/Users/snehs/apps.exe')
        sftp.close()

        stdout = client.exec_command('runthis.exe')[1]

        for line in iter(stdout.readline, ""):
            print(line, end='')
            with open("outfile.csv", 'a') as outfile:
                outfile.write(line)

        stdin, stdout, stderr = client.exec_command('del 111.csv') 
  ```
    
## [Link](https://docs.google.com/document/d/1k7fxpWDZwtPqo_2-B4cer3tLjnJlHR41NVH0OvFeclw/edit?usp=sharing) for more info


