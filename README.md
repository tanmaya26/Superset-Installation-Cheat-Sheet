# Superset-Installation-Cheat-Sheet
Steps to install Superset on Amazon EC2 Linux version 1 machine

>NOTE: As of May 2019, Superset works on python ~= 3.6 versions. You will find the following error if you have python versions < 3.6.
>ERROR: Complete output from command python setup.py egg_info:
>ERROR: Sorry, Python < 3.6 is not supported
>So, make sure you use the right version by running the command: python -V

Here, my instance is a Linux version 1 machine. All commands to be executed with sudo.


## STEPS
>sudo yum update -y <br>
>sudo yum install python36 -y

### Add below lines to ~/.bashrc

   >export PATH=/usr/local/bin:$PATH <br>
   >alias python=python36 <br>
   
>source ~/.bashrc

### Execute the following commands for PIP and OS dependencies
Your pip is now in /usr/bin/pip-3.6 because you installed python3.6
Always make sure to upgrade setuptools and python tools as we did here.
>sudo yum install python36-pip  -y <br>
>sudo /usr/bin/pip-3.6 install --upgrade setuptools pip <br>
>sudo yum upgrade python-setuptools -y <br>
>sudo yum install gcc gcc-c++ libffi-devel python-devel python-pip python-wheel openssl-devel libsasl2-devel openldap-devel -y <br>
>sudo yum install python36-devel -y <br>
>sudo cp /usr/local/bin/pip /usr/sbin/ <br>

### Following steps will install Superset
>sudo pip install superset <br>
>fabmanager create-admin --app superset <br>

Add admin by username, first name, last name and password. Make sure you remember this. <br>

NOTE: If following error occurs: "Was unable to import superset Error: cannot import name may_box_datetimelike", then it could be because a conflicting version of Pandas. Do the following:
sudo pip uninstall pandas <br>
sudo pip install pandas==0.23.4 <br>
After reinstalling pandas, repeat above.<br>

>superset db upgrade
If this step fails with following: "sqlalchemy.exc.InvalidRequestError: Can't determine which FROM clause to join from", then try with the following command:<br>
>sudo pip install sqlalchemy==1.2.18 <br>
then run again

>superset load_examples
>superset init
>superset runserver -d













