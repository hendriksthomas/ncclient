ncclient: Python library for NETCONF clients
--------------------------------------------

`ncclient` is a Python library that facilitates client-side scripting
and application development around the NETCONF protocol. `ncclient` was
developed by [Shikar Bhushan](http://schmizz.net). It is now maintained
by [Leonidas Poulopoulos](http://ncclient.grnet.gr)

This version includes a merge of [Juniper Networks](http://www.juniper.net)
and [Cisco Systems](http://www.cisco.com) respective ncclient forks based
on [leopoul/ncclient v0.3.2](https://github.com/leopoul/ncclient)

#### Requirements:
* Python 2.6 <= version < 3.0
* setuptools 0.6+
* Paramiko 1.7+
* lxml 3.0+
* libxml2 (libxml2-dev on Ubuntu/Debian)
* libxslt (libxslt1-dev on Ubuntu/Debian)

#### Installation:

    [ncclient] $ sudo python setup.py install

#### Examples:

    [ncclient] $ python examples/juniper/*.py

### Usage
#####Get device running config
Use either an interactive Python console (ipython)
or integrate the following in your code:

    from ncclient import manager

    with manager.connect(host=host, port=22, username=user, hostkey_verify=False) as m:
        c = m.get_config(source='running').data_xml
        with open("%s.xml" % host, 'w') as f:
            f.write(c)

As this version integrates Juniper's and Cisco's forks,
lots of new concepts have been introduced that ease
management of Juniper and Cisco devices respectively.
The biggest change is the introduction of device handlers
via the param ***name*** in connection. For example to invoke
Juniper's functions annd params one has to re-write the
above with name = ***junos***:

    from ncclient import manager

    with manager.connect(host=host, port=22, username=user, hostkey_verify=False, name='junos') as m:
        c = m.get_config(source='running').data_xml
        with open("%s.xml" % host, 'w') as f:
            f.write(c)

Respectively, for Cisco nxos, the name is ***nxos***.
Device handlers are easy to implement and prove to be futureproof.

### Changes | brief
* Switch between replies if custom handler is found
* Add Juniper, Cisco and default device handlers
* Allow preferred SSH subsystem name in device params
* Allow iteration over multiple SSH subsystem names.