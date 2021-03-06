
[![Build Status](https://travis-ci.org/ICTatRTI/ict-chef-repo.png?branch=master)](https://travis-ci.org/ICTatRTI/ict-chef-repo)


Quick Setup
==========


1. git clone git@github.com:ICTatRTI/ict-chef-repo.git
2. cd ict-chef-repo
3. vagrant up
4. Go to http://localhost:8888


Common workstation tasks
=============

Configure Knife
`knife configure`

Bootstrap a tangerine node
`knife bootstrap -i ~/keys/ictadmin_rsa 192.241.212.68 -N test-node -r role[base] --sudo`


Other useful information
=============

Sample knife.rb
```
current_dir = File.dirname(__FILE__)
log_level :debug
log_location STDOUT
node_name 'adampreston'
client_key '/Users/adampreston/Repository/ict-chef-repo/.chef/adampreston.pem'
validation_client_name 'chef-validator'
validation_key '/etc/chef/chef-validator.pem'
chef_server_url 'https://chef-server.idg-rti.org'
cache_type 'BasicFile'
cache_options( :path => '/Users/adampreston/Repository/ict-chef-repo/.chef/checksums' )
cookbook_path ["#{current_dir}/../cookbooks"]
cookbook_copyright "Research Triangle Institute."
cookbook_license "apachev2"
cookbook_email "apreston@rti.org"
``` 




