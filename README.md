This repository container script for running custom certifying authority (CA) for inferno OS. Can respond to requests which are in format: 

    getauthinfo <server> <signer> <username> <password>

Usage:

0.  Update docker image

        docker pull dievri/inferno-os:changelogin_noninteractive

1.  Clone repository and cd to 9mine-auth

        git clone https://github.com/9mine/9mine-auth.git && cd 9mine-auth

2.  Run script

        ./auth.sh <name> <password>

    where `<name>` is name of the local CA and `<password>` - password of the local CA.

    This command will run inferno inside docker container and setup it for using as CA. By default, `signerkey` and `keys` will be stored in `keydb` directory oh host machine.

InfernoOS exports `cmd` and `newuser` [file2chan](http://www.vitanuova.com/inferno/man/1/sh-file2chan.html) files.

`cmd` executes everything written to its. Response of execution can be obtained by reading `cmd`.

`newuser` file expecting write to it in the following format:

        <username> <password> <privileges>

and stores `username` in `users` directory, `password` in file `users/<username>/password` and `privileges` in file `users/<username>/privs` on host machine.

By default this files exported on port `1917` inside container and listening on port `42421` outside container.

Everything can be customized by editing `auth.sh` or/and `profile` files. 
