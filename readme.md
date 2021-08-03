# Unofficial Flora Docker Container
Source Code: https://github.com/lryanuk/chia-docker/tree/flora

## Basic Startup
```
docker run --name <container-name> -d lryanuk/flora-docker:latest
(optional -v /path/to/plots:/plots)
```
#### set the timezone for the container (optional, defaults to UTC)
Timezones can be configured using the `TZ` env variable. A list of supported time zones can be found [here](http://manpages.ubuntu.com/manpages/focal/man3/DateTime::TimeZone::Catalog.3pm.html)
```
-e TZ="America/Chicago"
```
## Configuration

You can modify the behavior of your flora container by setting specific environment variables.

To use your own keys pass as arguments on startup (post 1.0.2 pre 1.0.2 must manually pass as shown below)
```
-v /path/to/key/file:/path/in/container -e keys="/path/in/container"
```
or pass keys into the running container
```
docker exec -it <container-name> venv/bin/flora keys add
```
alternatively you can pass in your local keychain, if you have previously deployed flora with these keys on the host machine
```
-v ~/.local/share/python_keyring/:/root/.local/share/python_keyring/
```
or if you would like to persist the entire mainnet subdirectory and not touch the key directories at all
```
-v ~/.flax/mainnet:/root/.flax/mainnet -e keys="persistent"
```

To start a farmer only node pass
```
-e farmer="true"
```

To start a harvester only node pass
```
-e harvester="true" -e farmer_address="addres.of.farmer" -e farmer_port="portnumber" -v /path/to/ssl/ca:/path/in/container -e ca="/path/in/container" -e keys="copy"
```

The `plots_dir` environment variable can be used to specify the directory containing the plots, it supports PATH-style colon-separated directories.

#### or run commands externally with venv (this works for most flora XYZ commands)
```
docker exec -it flora venv/bin/flora plots add -d /plots
```

#### status from outside the container
```
docker exec -it flora venv/bin/flora show -s -c
```

#### Connect to testnet?
```
docker run -d --expose=58444 --expose=8555 -e testnet=true --name <container-name> lryanuk/flora-docker:latest
```

#### Need a wallet?
```
docker exec -it flora-farmer1 venv/bin/flora wallet show (follow the prompts)
```
