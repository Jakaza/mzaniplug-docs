# EC2 Problem 01 Space used up on EC2

## Problem
The application was down

## SSH Connection
```bash
Goodness@Zim-GChauke-Laptop MINGW64 ~/documents/github
$ ssh -i "mzansiplug_keypair.pem" ubuntu@54.159.177.219
Welcome to Ubuntu 24.04.2 LTS (GNU/Linux 6.8.0-1029-aws x86_64)

* Documentation:  https://help.ubuntu.com
* Management:     https://landscape.canonical.com
* Support:        https://ubuntu.com/pro

System information as of Fri Jul  4 11:24:41 UTC 2025

System load:  0.26              Processes:             111
Usage of /:   99.8% of 6.71GB   Users logged in:       0
Memory usage: 27%               IPv4 address for enX0: 172.31.87.92
Swap usage:   0%

=> / is using 99.8% of 6.71GB

Expanded Security Maintenance for Applications is not enabled.

18 updates can be applied immediately.
11 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status

*** System restart required ***
Last login: Wed Jun 25 10:36:35 2025 from 18.206.107.27
```

# Solution
Clean The EC2 Space Usage
Find large files/folders:
```
sudo du -h --max-depth=1 / | sort -hr | head -20
```

Delete logs or temporary files:
```
sudo journalctl --vacuum-time=2d
sudo rm -rf /var/log/*.gz /var/log/*.[0-9]
sudo apt-get clean
```

Check what's using space (/home):
```
du -sh /home/*
```

List Large Files (Over 10MB):
```
find . -type f -size +10M -exec du -h {} + | sort -hr | head -30
```

Had two virtual environments:
venv (937MB)
nenv (937MB)
Deleted one:
```
rm -rf /home/ubuntu/mzansiplug/venv
```

Deployment
Made some changes on my local and pushed:
- Since I have GitHub Action to automate the deployment, everything went well
- It restarted Gunicorn and Nginx
- And set up everything needed

