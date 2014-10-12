ufw-formula
===========

This module manages your firewall using ufw with pillar configured rules.

See the full [Salt Formulas installation and usage instructions](http://docs.saltstack.com/topics/development/conventions/formulas.html).

Usage
-----

All the configuration for the firewall is done via pillar (pillar.example).

Enable firewall, applying default configuration:
```javascript
ufw:
  enabled: True
```

Allow 80/tcp (http) traffic from only two remote addresses:
```
ufw:
  services:
    http:
      protocol: tcp
      from_addr:
        - 10.0.2.15
        - 10.0.2.16
```

Allow 443/tcp (https) traffic from network 10.0.0.0/8 to an specific local ip:
```
ufw:
  services:
    https:
      protocol: tcp
      from_addr:
        - 10.0.0.0/8
      to_addr: 10.0.2.1
```

Allow from a service port:
```
ufw:
  services:
    smtp:
      protocol: tcp
```

Allow from an specific port, by number:
```
ufw:
  services:
    139:
      protocol: tcp
```

Allow from a range of ports, udp:
```
ufw:
  services:
    "10000:20000":
      protocol: udp
```

Allow from two specific ports, udp:
```
ufw:
  services:
    "30000,40000":
      protocol: udp
```

Allow an application defined at /etc/ufw/applications.d/:
```
ufw:
  applications:
    - OpenSSH
```

Authors
-------

Original state and module based on the work from [Yigal Duppen](https://github.com/publysher/infra-example-nginx/tree/develop).

Salt formula developed by Mario del Pozo.

