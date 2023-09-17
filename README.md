* support https://radicle.zulipchat.com
  * stream: #support
  * topic: "protocol.berg"

* requirements
  * git >= 2.34
    ```
    git --version
    ```
  * require openssh 9.1 or layer with ssh-agent
    ```
    ssh -V
    ssh-agent
    ```

* workshop
  * app.radicle.xyz/nodes/seed.radicle.garden

* protocol berg
  * https://app.radicle.xyz/nodes/seed.radicle.garden/rad:zXuTcNc31sGFA7Ts7F93D2c5NNAG

* run Radicle node
```bash
sudo docker container run --name radicle -it alpine 
apk add openssh git curl tar
export SHELL="/bin/ash"
sh <(curl -sSf https://radicle.xyz/install)
printf "PATH="$PATH:/root/.radicle/bin" >> ~/.profile
source ~/.profile
export PATH="$PATH:/root/.radicle/bin"
```

* show help
```
rad --help
```

* initialise identity
```
rad auth
rad self
```

* backup Radicle keys 
```
cp /root/.radicle/keys/radicle /root/.radicle/keys/radicle-backup
chmod 777 /root/.radicle/keys/radicle-backup
sudo docker cp radicle:/root/.radicle/keys/radicle.pub ~/Desktop/radicle.pub
sudo docker cp radicle:/root/.radicle/keys/radicle-backup ~/Desktop/radicle
```

* initialize new project
```
rad init
```

* clone and run protocol berg did repo
```
rad clone rad:zXuTcNc31sGFA7Ts7F93D2c5NNAG
rad self
rad node start --foreground
rad node status
```

* reenter docker container of radicle after exiting it
```
docker start radicle
docker exec -it radicle /bin/ash
```

* demo

```
gco -b workshop
vim thanks.md
gst
ga .
ga -m "thanks
gst
tig
# push to rad node
# add a patch message in vim
# may also use `rad patch --all`
git push rad HEAD:refs/patches
rad patch
rad patch show <COMMIT>
```
