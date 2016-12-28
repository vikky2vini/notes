## Chef

###### Set up chef on a workstation (to adminstrate other nodes):
  1.) Ensure root login is enabled for the first convergence
  2.) Make sure curl is installed
  3.) `curl -L https://www.opscode.com/chef/install.sh | sudo bash`

###### Install chef on a node:
  `$ knife bootstrap <hostname or IP address> -x username -P password -N "nodename"`

###### Show details regarding a node:
  `$ knife node show <node-name>`
  `$ Note: -l gives you more info`

###### Create a cookbook:
  `$ knife cookbook create <cookbookname>`

###### Remove a cookbook:
  `$ knife cookbook delete <cookbookname>`

###### Create a data bag:
  `$ knife data_bag from file users jay.json`

###### Add a recipe to a node's run list:
  `$ knife node run_list add chef-test-node "recipe[del_val]"`

###### Creating a role:
  * Add `role_name.rb` to roles directory
  * Upload the role: `$ knife node role from file roles/server.rb`

###### Add a node to a role:
  `$ knife node run_list add fqdn "role[role_name]"`

###### Remove a recipe from a node's run list:
  `$ knife node run_list remove chef-test-node "recipe[config_ssh_jay_authkeys]"`

###### Display list of currently configured nodes:
  `$ knife client list`

###### Edit a node directly:
  `$ knife node edit <node-name>`