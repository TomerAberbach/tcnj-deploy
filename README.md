# TCNJ Deploy

> A bash script for easily deploying a directory of website files to your personal TCNJ website at https://www.tcnj.edu/~username.

## Install

If you have `curl` installed (or can install it by running `sudo apt install curl`):

```sh
$ sudo curl -o /usr/bin/tcnj-deploy https://raw.githubusercontent.com/TomerAberbach/tcnj-deploy/master/tcnj-deploy.sh
```

Otherwise download the [script](https://raw.githubusercontent.com/TomerAberbach/tcnj-deploy/master/tcnj-deploy.sh) and rename/move it to `/usr/bin`:

```sh
$ sudo mv tcnj-deploy.sh /usr/bin/tcnj-deploy
```

Lastly, make the file executable:

```sh
$ sudo chmod +x /usr/bin/tcnj-deploy
```

## Usage

```sh
$ tcnj-deploy <directory>
```

Your `~/www` directory is cleared prior to copying your files so use with caution!

The proper permissions are set on your copied files for you.

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
