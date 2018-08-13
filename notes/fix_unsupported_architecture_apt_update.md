
## Some issues with apt-get update

### Fix an issue with unsupported architecture 

If your native architecture is `amd64`
```console
$ sudo dpkg --print-architecture 
```
and you got a message like this
```text
N: Skipping acquire of configured file 'stable/binary-i386/Packages' as repository 'https://download.docker.com/linux/ubuntu xenial InRelease' doesn't support architecture 'i386'
```
you need to add `[arch=amd64]` before a repository URL
```text
deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable
```
