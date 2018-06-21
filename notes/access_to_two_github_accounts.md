
## Setting up access to two GitHub accounts

### Set up the first (default) account

Create a new ssh key if you don't have it
```console
$ ssh-keygen -t rsa -b 4096 -C "first_account@example.com"
```

Accept the default key location and skip using a passphrase
```text
Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
Enter passphrase (empty for no passphrase): [Press enter]
Enter same passphrase again: [Press enter]
```

Add the key to the ssh-agent
```console
$ ssh-add -k
```

Sign in to your first profile on GitHub and add the key
```text
Settings -> SSH and PGP keys -> New SSH key
```

Check it
```console
$ ssh -T git@github.com
```

### Set up another account

Create another ssh key
```console
$ ssh-keygen -t rsa -b 4096 -C "second_account@example.com"
```

Set a file name for the second key and skip using a passphrase
```text
Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [ /Users/you/.ssh/second_key ]
Enter passphrase (empty for no passphrase): [Press enter]
Enter same passphrase again: [Press enter]
```

Add the second key to the ssh-agent
```console
$ ssh-add -k /Users/you/.ssh/second_key
```

Sign in to your second profile on GitHub and add the second key
```text
Settings -> SSH and PGP keys -> New SSH key
```

Add lines to your ssh client config (/Users/you/.ssh/config)
```text
Host github.second
    HostName github.com
    IdentityFile /Users/you/.ssh/second_key
```

Check it
```console
$ ssh -T git@github.second
```
