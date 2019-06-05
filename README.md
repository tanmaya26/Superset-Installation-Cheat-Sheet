# Superset-Installation-Cheat-Sheet
Steps to install Superset on Amazon EC2 Linux version 1 machine <br>
NOTE:
>As of May 2019, Superset works on python ~= 3.6 versions. You will find the following error if you have python versions < 3.6.<br>
>ERROR: Complete output from command python setup.py egg_info <br>
>ERROR: Sorry, Python < 3.6 is not supported
>So, make sure you use the right version by running the command: python -V

Here, my instance is a Linux version 1 machine. All commands to be executed with sudo.


## STEPS
```
sudo yum update -y
```
```
sudo yum install python36 -y
```

### Add below lines to ~/.bashrc
```
export PATH=/usr/local/bin:$PATH
alias python=python36
```
```
source ~/.bashrc
```
### Execute the following commands for PIP and OS dependencies
Your pip is now in /usr/bin/pip-3.6 because you installed python3.6
Always make sure to upgrade setuptools and python tools as we did here.
```
sudo yum install python36-pip  -y 
sudo /usr/bin/pip-3.6 install --upgrade setuptools pip 
sudo yum upgrade python-setuptools -y 
sudo yum install gcc gcc-c++ libffi-devel python-devel python-pip python-wheel openssl-devel libsasl2-devel openldap-devel -y 
sudo yum install python36-devel -y 
sudo cp /usr/local/bin/pip /usr/sbin/ 
```
### Following steps will install Superset
Install Superset inside virtualenv

```
sudo pip install virtualenv
```

```
python3 -m venv venv
```

Start/Activate virtualenv
```
. venv/bin/activate
```
Now, install superset
```
sudo pip install superset
```
Add admin by username, first name, last name and password. Make sure you remember this. <br>
```
fabmanager create-admin --app superset
```

NOTE:
>If following error occurs in above step: "Was unable to import superset Error: cannot import name may_box_datetimelike", then it could be because a conflicting version of Pandas. Do the following:
>>sudo pip uninstall pandas <br>
>>sudo pip install pandas==0.23.4<br>
>After reinstalling pandas, repeat above step.<br>

Initialize the database
```
superset db upgrade
```
NOTE:
>If this step fails with following: "sqlalchemy.exc.InvalidRequestError: Can't determine which FROM clause to join from", then try with the following command:<br>
>>sudo pip install sqlalchemy==1.2.18<br>
>then run again<br>

Load some data to play with
```
superset load_examples
```
Create default roles and permissions
```
superset init
```
Start the web server on port 8088, use -p to bind to another port
```
superset runserver -p 8088
```
Connect to URL after configuring port on EC2 settings

```
http://<EC2 public DNS>:8088/
```













