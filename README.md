# chefserver
# Create Account on  Public chef Server

```bash
https://manage.chef.io/
````
```bash
1) Create Account
2) Login to Account
3) Create Orgnization
4) Download Stater kits under the Organization as chef-starter.zip
5) Exract chef-starter.zip to D:\
6) copy Chef-repo folder to D: like D:\chef-repo
````

# On Chef Workstation
```bash
#open Chefworkstation powershell
#go to D:\chef-repo
#check Connection between Chef Workstation & Chef Client
E:\chef-repo>knife ssl check
````
if Above command Get error then follow below steps

```bash
if above command get error try below command & try Again
below command help you to fetch ssl certificate from chef server
and install on chef workstation
E:\chef-repo>knife ssl fetch
````

# Generate cookbook
```bash
E:\chef-repo\cookbooks>chef generate cookbook 123-cookbook
````

# Generate recipe inside cookbook

```bash
1) E:\chef-repo\cookbooks\123-cookbook>chef generate recipe demo
# write code in to E:\chef-repo\cookbooks\123-cookbook\recipe\demo.rb

Example
file 'c:\myfile' do
content 'Test recipe from kalpesh welcome to charusat updated cookbook'
action :create
end

service 'CharusatApps' do
action [:enable, :start]
end

windows_package 'winscp' do
action	:add
source 'http://kalpeshpc:8080/WinSCP-5.15.5-Setup.exe'
  
end

powershell_script 'Shutdown PC' do
  code <<-EOH
   shutdown -r -f -t 00
  EOH
 end


````

# To check syntax error
```bash
chef exec ruby -c .\123-cookbook\recipes\demo.rb
````

# Optional Step
```bash
To check recipe on locale server of chefworkstation
# Command is below
chef-client -zr "recipe[123-cookbook::demo]"
````

# Upload cookbook to chef server
```bash
E:\chef-repo> knife cookbook upload 123-cookbook
````

# Bootstraping of windows chef Client

```bash
Bootstraping is process to add chef client in to chefserver
E:\chef-repo>knife bootstrap -o winrm 172.16.2.36 -N '716A-11' -U Administrator -P 'password'
````

# Bootstraping of windows chef Client without SSL Certificate
knife bootstrap -o winrm 172.16.2.39 -N 'ip/pcname' -U Administrator -P 'password' --winrm-no-verify-cert

# On Chef Client
```bash
Manually Download Recipe task from Chef Server
C:\User\Administrator> chef-client
````


