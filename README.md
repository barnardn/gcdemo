# GCDemo

## Repository for demoing git-crypt

### Steps to create this repository

On a different computer, I created this repository, and set up git-crypt to 
encrypt the files in the `secrets/` directory:

    $ cd gcdemo
    $ git init          # initialize a git repository
    $ git-crypt init    # initialize the repository to use git-crypt
    $ git-crypt add-pgp-user <identity hash> # added myself as a colaborator
    
I added myself as a collaborator so that I could read the encrypted files.
    
Next I created a `.gitattributes` file in `secrets/` with the following entries:

    apikeys.txt filter=git-crypt diff=git-crypt  ## encrypt a speficic file
    secret* filter=git-crypt diff=git-crypt      ## encrypt files matching a pattern
    

I then committed my changes and pushed to github.  The files matching the `secret` 
pattern as well as `apikeys.txt` are encrypted to everyone but me.  To add another
collaborator (say my Dox work account). I imported my Dox gnupg key into my keychain:

    $ gpg --search nbarnard@doximity.com
    gpg: searching for "nbarnard@doximity.com" from hkps server hkps.pool.sks-keyservers.net
    (1)     Norm Barnard <nbarnard@doximity.com>
              4096 bit RSA key EC7C6A9C, created: 2018-02-25, expires: 2019-02-25
    (2)     Norm Barnard <nbarnard@doximity.com>
              4096 bit RSA key 1648F3C8, created: 2017-01-02

    Keys 1-2 of 2 for "nbarnard@doximity.com".  Enter number(s), N)ext, or Q)uit > 1
    
For the live part of the demo, on my other laptop I will add my Dox account 
as a collaborator:

    git-crypt add-gpg-user nbarnard@doximity.com
    
committed and pushed the changes to github.

And back on my work laptop, pull and unlock.


