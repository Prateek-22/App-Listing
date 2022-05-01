# App-Listing

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


