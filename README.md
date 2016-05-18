Simple POC Locust environment with Berkshelf Chef and Vagrant support

Requirements
------------
* chef-dk
* chef-solo
* berkshelf

Extra development requirements
-----------------------------
* vagrant
* virtualbox

Resources links
---------------
* Chef DK(includes Berkshelf): https://downloads.getchef.com/chef-dk/
* Vagrant: https://www.vagrantup.com/downloads.html
* Virtualbox: https://www.virtualbox.org/wiki/Downloads

Guide
-----

* Make sure you have the requierments above installed
* Clone this repo
* Inside the cloned repo run "kitchen converge"
* After the machine is provisioned, your locust gui will be available at http://192.168.4.2:8089/

* The example role is currently testing some of the locust io wiki pages:

roles/locust.json
```
{
    "name": "locust",
    "chef_type": "role",
    "json_class": "Chef::Role",
    "description": "Locust behaviour",
    "run_list": [
        "recipe[locust-swarm]"
    ],
    "default_attributes": {
        "locustio": {
            "base_url": "docs.locust.io",
            "uri_list": [
                {
                    "uri": "/en/latest/",
                    "weight": 10,
                    "identifier": "latest"
                },
                {
                    "uri": "/en/latest/what-is-locust.html",
                    "weight": 5,
                    "identifier": "about"
                },
                {
                    "uri": "/en/latest/installation.html",
                    "weight": 2,
                    "identifier": "install"
                }
            ]

        }
    }
}
```

* You can setup your own test by altering the values in the example above
* The base_url and uri are self explanatory
* The weight controls the request distribution
* The identifier must be unique
* Another kitchen converge needs to be run in order to update the locust test file

Credits
-------
* You can find the main locust cookbook here: https://supermarket.chef.io/cookbooks/locustio