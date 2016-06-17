docker-blackbox
---------------

Docker image for playing with [StackExchange/blackbox](https://github.com/StackExchange/blackbox)

**see hub.docker.com/r/dylanmei/blackbox**

# example

create a keypair for admin@example.com

```
mkdir -p /tmp/gnupg
docker run --rm -it -v /tmp/gnupg:/gnupg dylanmei/blackbox gpg --gen-key
```

list keys

```
docker run --rm -t -v /tmp/gnupg:/gnupg dylanmei/blackbox gpg --list-keys
```

init a repo

```
mkdir -p /tmp/repo
cd /tmp/repo
git init
docker run --rm -it -v /tmp/repo:/repo dylanmei/blackbox blackbox_initialize
``

add an admin

```
docker run --rm -t -v /tmp/repo:/repo -v /tmp/gnupg:/gnupg dylanmei/blackbox blackbox_addadmin admin@example.com
```

encrypt file

```
echo "hello blackbox" > /tmp/repo/hello.txt
docker run --rm -t -v /tmp/repo:/repo -v /tmp/gnupg:/gnupg dylanmei/blackbox blackbox_register_new_file hello.txt
```

decrypt file

```
docker run --rm -it -v /tmp/repo:/repo -v /tmp/gnupg:/gnupg dylanmei/blackbox blackbox_cat hello.txt
```
