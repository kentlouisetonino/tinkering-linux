## Manually compile the app.
```sh
g++ -o app src/app.cpp
```

<br />
<br />



## Run the multipass.

```sh
sudo systemctl restart snap.multipass.multipassd.service
```

<br />
<br />



## Deploy to snap store.
```sh
snapcraft login
snapcraft register bus-calculator
snapcraft clean
snapcraft
snapcraft push bus-calculator_<version-number-in-snapcraft-yaml>_amd64.snap --release=stable
```
