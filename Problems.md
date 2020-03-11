
# Encoutered Problems

## 1. Environment

### Docker

For deployment convenience, I buildup a docker container. With the tool, it can easily run the PoA blockchain network.

#### **[Install](https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl) `docker-compose` onRaspberry Pi**

1. Install Docker

   ```bash
   curl -sSL https://get.docker.com | sh
   ```

2. Add permission to pi (or use root)

   ```bash
   sudo usermod -aGdocker pi
   ```

3. Test Docker installation

   ```bash
   docker run hello-world
   ```

4. Install proper dependencies

   ```bash
   sudo apt-get install libffi-dev libssl-dev
   
   sudo apt-get install -y python python-pip
   
   sudo apt-get remove python-configparser
   ```

5. Install Docker Compose

   ```bash
   sudo pip install docker-compose
   ```

   **Note**: use python3 and pip3. To check the version, use `which python`, `which pip`

#### Problems

- [x] **Problem 1: **

```python
pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.
```

**Cause：**

The network speed is too slow for the default timeout of `pip`.

**Solution:**

```bash
pip install docker-compose --default-timeout=1000
```

- [x] ~~**Problem 2:**~~

```bash
root@raspberrypi:/home/pi/Documents/wifi-devnet# docker-compose up
Pulling node (ethereum/client-go:alltools-release-1.8)...
ERROR: Get https://registry-1.docker.io/v2/: net/http: TLS handshake timeout
```

~~**Cause:**~~

~~`net/http: TLS handshake timeout` caused by slow internet connection. Unfortunately docker don't have any settings that allows you change connection timeout.~~

~~**Solution:** `reboot`~~

- [ ] **Problem 3:**

```bash
root@raspberrypi:/home/pi/Documents/wifi-devnet# docker-compose up
Starting wifi-devnet_node_1 ... done
Attaching to wifi-devnet_node_1
node_1  | standard_init_linux.go:211: exec user process caused "exec format error"
wifi-devnet_node_1 exited with code 1
```

**Possible Cause:**

1. - [x] ~~Use the non-linux line seperator `\r\n`~~  

2. - [ ] 32-bit OS.

