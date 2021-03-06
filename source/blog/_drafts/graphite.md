---
collection: blog

draft: true
date: 2013-07-11

template: post.html
---


## Overview
Graphite is made of 3 components (all python);
- [Carbon](); is the gatherer service, it receives data and transfer them to the storage whisper
- [Whisper](); is the storage database, it stores data in a format similar to RRD; into individual files 
- [Graphite-web](); is a django webapp used to query whisper and returns either JSON (used in canvas) or directly pictures.

Available documentation available [here](http://graphite.readthedocs.org/en/latest)

## Requirements
Graphite can either be installed from source, pip or in virtualenv (python isolation).
We prefer the [pip](https://pypi.python.org/pypi/pip) approach because .. it's the python package manager.

- Ensure pip is installed

```
sudo apt-get install -y python-pip
```

- Ensure python development package is installed to build carbon

```
sudo apt-get install -y python-dev 
```

## Steps
- Install the Graphite components, using the default path (/opt/graphite)
```
sudo pip install whisper  # note the binary will be installed in /usr/local/bin
sudo pip install carbon
sudo pip install graphite-web
```
**Note**: Options are available to pip to perform installation in other location, see [manual](http://graphite.readthedocs.org/en/latest/install-pip.html)

- Since graphite-web is based on django, we need to install it and a tag lib for tagging the database, a graphics library to generate graphs.
```
pip install django==1.3  # 1.3 will save you a lot of trouble if you haven't tried django before
pip install django-tagging
sudo apt-get install python-cairo
```

- Initialize the database
```
cd /opt/graphite/webapp/graphite/ && sudo python manage.py syncdb
```
Django will likely want you to create some kind of admin account, just go ahead and do that too.

- Configure Carbon, currently we can use the default values in the examples
```
cd /opt/graphite/conf && sudo cp carbon.conf.example carbon.conf
cd /opt/graphite/conf && sudo cp storage-schemas.conf.example storage-schemas.conf
```
**Note**: By default, data will be saved for 1 day in 1 minute intervals. Refer [here](http://graphite.readthedocs.org/en/latest/config-carbon.html#storage-schemas-conf) to see how to modify data retentions.

- Start the data collection daemon
```
cd /opt/graphite && sudo ./bin/carbon-cache.py start
```
and run the web interface under the django development server
```
cd /opt/graphite && sudo ./bin/run-graphite-devel-server.py .
```
By default the server will listen on port 8080, point your web browser at http://127.0.0.1:8080/ to bring up the graphite webapp and start creating graphs(if [collectd](https://github.com/devo-ps/api.devo.ps/wiki/Collectd) is running and configured correctly)!.

## Troubleshooting

- Carbon-cache can be run in the debug mode
```
cd /opt/graphite && sudo ./bin/carbon-cache.py --debug start
```

- So is django
```
echo DEBUG = True >> /opt/graphite/webapp/graphite/local_settings.py
```

- Or, try this to watch the various logs if something is not working right:
```
cd /opt/graphite && find . -name '*.log' | xargs tail -F
```
