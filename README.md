# TCNJ Deploy

A bash script for easily deploying a directory of website files to your personal TCNJ website at https://www.tcnj.edu/~username.

Usage:
```shell
$ ./tcnj-deploy <directory>
```

Your `~/www` directory is cleared prior to copying your files so use with caution!

The proper permissions are set on your copied files for you.

The code can be seen here:
```bash
#!/usr/bin/env bash

if [[ -d "$1" ]]; then
    read -p "This will overwrite everything in '~/www' with the contents of '$1'. Continue? (y/n) " -n 1 -r
    echo

    if [[ $REPLY =~ ^[Yy]$ ]]; then
        read -p "Username: " -r username
        tar -c -C $1 . | gzip -2 | ssh -o ConnectTimeout=10 "$username@beauty.tcnj.edu" "rm -rf ~/www > /dev/null; mkdir -p ~/www; tar -zx -C ~/www; wwwsetup > /dev/null; chmod -R +rxX ~/www; echo; echo \"Deployment successful!\""
        
        if [[ $? -ne 0 ]]; then
            echo
            echo "Deployment failed!"
            echo "In order to use this command you must be connected to the TCNJ network or using a VPN."
            
            if [[ "$(uname)" == "Darwin" ]]; then
                echo "Mac VPN Tutorial: http://nts.pages.tcnj.edu/files/2014/08/PAN-VPN-Instructions.pdf"
            elif [[ "$(expr substr $(uname -s) 1 5)" == "Linux" ]]; then
                echo "Linux VPN Tutorial: http://tomeraberbach.com/html/article/tcnj-linux-vpn.html"
            else
                echo "Windows VPN Tutorial: http://nts.pages.tcnj.edu/files/2014/08/PAN-VPN-Instructions.pdf"
            fi
        fi
    fi
else
   echo "Usage: ./tcnj-deploy.sh <directory>"
fi
```
