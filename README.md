# chefserver
# for Public chef Server go to
https://manage.chef.io/
# Create Account
#Login to Account
#Crete orgnization
#Download Stater kits under the Organization as chef-starter.zip
#Exract chef-starter.zip to D:\
#copy Chef-repo folder to D: like D:\chef-repo


On Chef Workstation
#open Chefworkstation powershell
#go to D:\chef-repo
#check Connection between Chef Workstation & Chef Client
E:\chef-repo>knife ssl check

# if above command get error try below command & try Again
#below command help you to fetch ssl certificate from chef server
# and install on chef workstation
E:\chef-repo>knife ssl fetch

# Generate cookbook
E:\chef-repo\cookbooks>chef generate cookbook 123-cookbook

# Generate recipe inside cookbook
E:\chef-repo\cookbooks\123-cookbook>chef generate recipe demo

# write code in to E:\chef-repo\cookbooks\123-cookbook\recipe\demo.rb
# Example
file 'c:\demofile' do
content 'my first recipe from kalpesh'
action :create
end

# To check syntax error
chef exec ruby -c .\123-cookbook\recipes\demo.rb

# option Step
# to check recipe on locale server of chefworkstation
# Command is below
chef-client -zr "recipe[123-cookbook::demo]"

#Upload cookbook to chef server
E:\chef-repo> knife cookbook upload 123-cookbook

#Bootstraping of windows chef Client
#Bootstraping is process to add chef client in to chefserver
E:\chef-repo>knife bootstrap -o winrm 172.16.2.36 -N '716A-11' -U Administrator -P 'ceit'


#Bootstraping of windows chef Client without SSL Certificate
knife bootstrap -o winrm 172.16.2.39 -N '716A-14' -U Administrator -P 'ceit' --winrm-no-verify-cert
On Chef Client
#Download Recipe task from Chef Server
C:\User\Administrator> chef-client
