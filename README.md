# apt-cacher-ng
A simple vagrant box with [apt-cache-ng](https://www.unix-ag.uni-kl.de/~bloch/acng/).
The apt-cache-ng is a caching proxy for deb packages.

# Quickstart
spin up a server with apt-cacher-ng
```
git clone https://github.com/joaocenoura/apt-cacher-ng.git apt-cacher-ng && cd $_
vagrant up
```

and configure clients by copying the file `conf/01_proxy` to clients folder `/etc/apt/apt.conf.d`

confirm that apt-cacher-ng is running and caching
```
vagrant ssh
...
sudo /etc/init.d/apt-cacher-ng status
tail -F /var/log/apt-cacher-ng/apt-cacher.*
```

and on the client side run a `sudo apt-get update`

apt-cacher-ng has a report page: http://192.168.33.254:3142/acng-report.html

# Configuration
the client configuration must point correctly to the server with apt-cacher-ng. just ensure the `Vagrantfile` has an accessible IP:
```
config.vm.network "private_network", ip: "192.168.33.254"
```

and edit clients configuration `01_proxy` to servers IP address:
```
Acquire::http { Proxy "http://192.168.33.254"; };
```
___
the provided acng.conf contains the following changes:
- PassThroughPattern: .* - allow connect to everything, particularly to HTTPS repos. note that deb fetched through HTTPS won't be cached