**Note:** There are modifications from a standard Magento release in this repo.  
For a clean stock Magento mirror: https://github.com/LokeyCoding/magento-mirror  


Magneto Mirror (Vagrant development/testing environment)
========================================================

Designed to be a fresh install of Magento, with the minium of variation from a standard package, for rapid depoloyment of a minimal environment for development and extension testing.  
This is in a working state for my purposes, but it should not be considered complete or bug free.  
This has only been tested with Mac OS X 10.8 and Windows 7 x64.  

Features
--------

* Vagrant support.
* Chef solo provisioner.
* Impliments the [vagrent_magento cookbook](https://github.com/rjocoleman/vagrant_magento)  
* Sample data download and install _(optional)_.  
  + Create's admin user.  
  + Aliased `/phpinfo.php` and `/magento-check.php` for _non-intrusive_ but basic debugging.  


Requirements
------------

* [Vagrant](http://vagrantup.com)  
* Vagrant required [Oracle's VirtualBox](http://www.virtualbox.org/)  


Variations from stock Magento
-----------------------------

* tealiumIQ module installed
* `README.md` added (this file).  
* `Vagrantfile`, `Cheffile` and `Cheffile.lock` in root directory.  
* `/deploy_support` and `/.librarian` folders.  
* `.gitignore` has been tightend up to cope with sample data and generated content.  


Installation
------------

* [Install Vagrant](http://vagrantup.com/v1/docs/getting-started/index.html) and you're ready to go.  


Usage
-----

* Clone this repo.
* `$ vagrant up` to start the virtual machine.  
* Navigate to http://127.0.0.1:1080/.  
* Ports `80` and `3306` are forwarded to `1080` and `13306` respectivly on your local machine (can be configured in your `Vagrantfile`).  

* `$ vagrant ssh` to connect to the virtual machine's console ([doesn't work on Windows](http://vagrantup.com/v1/docs/getting-started/ssh.html)).  
* `$ vagrant destroy` to delete all traces of the virutal environment.  

Further docs on Vagrant at [vagrantup.com](http://vagrantup.com/v1/docs/getting-started/teardown.html)  


Known Issues:
-------------

* When you first access Magento's admin, with `['sample_data']['install']` enabled you'll be greeted by an error report about the database table `vagrant_magento.catcha_log` not being created. Refreshing the page should give you access as the offending table is actually created at some point. This is a Magento (or sample data) bug and out of scope for this project.  


Configuration
-------------

These are some of the settings available. Default values are noted  
These are from the [vagrant_magento cookbook](https://github.com/rjocoleman/vagrant_magento).  

* `node['vagrant_magento']['phpinfo_enabled']` - Enable /phpinfo.php alias. Default is false.  
* `node['vagrant_magento']['mage_check_enabled']` - Enable /magento-check.php alias. Default is false.  

* `node['vagrant_magento']['sample_data']['install']` - Install Magento sample data. Default is false  

* `node['vagrant_magento']['config']['install']` - Install Magento. Default is false.  
* `node['vagrant_magento']['config']['db_name']` - Database. Default is "magento".  

* `node['vagrant_magento']['admin']['admin_username']` - Admin username. Default is "mage-admin".  
* `node['vagrant_magento']['admin']['admin_password']` - Admin password. Default is "abc1234"  
* `node['vagrant_magento']['admin']['admin_email']` - Admin email. Default is "test@example.com"  

These can be placed inside your `Vagrantfile` in `chef.json` e.g.
```ruby
chef.json = { 'vagrant_magento' => {
  'phpinfo_enabled' => true,
  'mage_check_enabled' => true,
  'sample_data' => { 'install' => true },
  'config' => { 'install' => true },
  'admin' => { 'admin_username' => 'robert', 'admin_password' => 'badpass1' }
  }

```


Contributing
------------

* *Note:* Most of the heavy lifiting is handled by the [vagrant_magento cookbook](https://github.com/rjocoleman/vagrant_magento) so that may be the best place to contribute.
* File bug reports via GitHub issues.
* Pull requests are welcome.
* [librarian](https://github.com/applicationsonline/librarian) is used to manage Chef dependancies. So pull requests probably won't be accepted for the `/cookbooks` folder.


Todo
----

* Add an option to use ZendServer CE as the base box.
* Support other Magento versions (branches)
* Compatibility with [vagrant-hostmaster](https://github.com/mosaicxm/vagrant-hostmaster).
* Cross platform testing.


License and Author
===================

* Author:: Robert Coleman <github@robert.net.nz>


* Copyright:: 2012

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
