# TCNJ Deploy

> A bash script for easily deploying a directory of website files to your personal TCNJ website at https://www.tcnj.edu/~username.

## Install

If you have `curl` installed (or can install it by running `sudo apt install curl`):

```sh
$ sudo curl -o /usr/bin/tcnj-deploy https://raw.githubusercontent.com/TomerAberbach/tcnj-deploy/master/tcnj-deploy.sh
```

Otherwise download the [script](https://raw.githubusercontent.com/TomerAberbach/tcnj-deploy/master/tcnj-deploy.sh) and rename/move it to `/usr/bin`:

```sh
$ sudo mv tcnj-deploy.sh /usr/bin/tcnj-deploy.sh
```

## Usage

```sh
$ tcnj-deploy.sh <directory>
```

Your `~/www` directory is cleared prior to copying your files so use with caution!

The proper permissions are set on your copied files for you.

The code can be seen here:
```bash
#!/usr/bin/env bash

if [[ -d "$1" ]]; then
    read -p "This will overwrite everything in '~/www' with the contents of '$1'. Continue? (y/n) " -n 1 -r
    echo
    echo

    if [[ $REPLY =~ ^[Yy]$ ]]; then
        read -p "Username: " -r username
        tar -c -C $1 . | gzip -2 | ssh -o ConnectTimeout=10 "$username@beauty.tcnj.edu" "rm -rf ~/www > /dev/null; mkdir -p ~/www; tar -zx -C ~/www; cd ~/www; find -type d -exec chmod 755 {} \;; find -type f -exec chmod 644 {} \;; echo; echo \"Deployment successful!\""
        
        if [[ $? -ne 0 ]]; then
            echo
            echo "Deployment failed!"
            echo "In order to use this command you must be connected to the TCNJ network or using a VPN."
            
            if [[ "$(uname)" == "Darwin" ]]; then
                echo "Mac VPN Tutorial: http://nts.pages.tcnj.edu/files/2014/08/PAN-VPN-Instructions.pdf"
            elif [[ "$(expr substr $(uname -s) 1 5)" == "Linux" ]]; then
                echo "Linux VPN Tutorial: https://tomeraberba.ch/post/article/tcnj-linux-vpn.html"
            else
                echo "Windows VPN Tutorial: http://nts.pages.tcnj.edu/files/2014/08/PAN-VPN-Instructions.pdf"
            fi
        fi
    fi
else
   echo "Usage: tcnj-deploy.sh <directory>"
fi
```

## Uninstall

Simply remove the the script file:

```sh
$ sudo rm /usr/bin/tcnj-deploy
```

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/TomerAberbach/tcnj-deploy/issues/new).

## Author

**Tomer Aberbach**

* [Github](https://github.com/TomerAberbach)
* [NPM](https://www.npmjs.com/~tomeraberbach)
* [LinkedIn](https://www.linkedin.com/in/tomer-a)
* [Website](https://tomeraberba.ch)

## License

Copyright © 2018 [Tomer Aberbach](https://github.com/TomerAberbach)
Released under the [MIT license](https://github.com/TomerAberbach/tcnj-deploy/blob/master/LICENSE).
