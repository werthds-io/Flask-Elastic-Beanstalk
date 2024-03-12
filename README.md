# Flask Elastic Beanstalk Demo

## Steps to install:

1. Clone the Flask-Elastic-Beanstalk repo
2. Set up a python virtual environment with Flask
2. Install, run and test the Flask application
3. Deploy the site with the AWS Elastic Beanstalk CLI (EB CLI)
4. Cleanup

### 3. Clone the Flask-Elastic-Beanstalk Demo

1. login to Github
2. Open the Flask-Elastic-Beanstalk repo
3. From "code" select the SSH clone link
4. Open local or Cloud9 Terminal

```
git clone git@github.com:werthds-io/Flask-Elastic-Beanstalk.git
```

### 2. Setup a python virtual environment with Flask

1. Create and activate a virtual environment
```
~$ cd Flask-Elastic-Beanstalk
~$ virtualenv virt
~$ source virt/bin/activate
(virt) ~/Flask-Elastic-Beanstalk$
```

2. Install Flask
```
(virt) ~/Flask-Elastic-Beanstalk$ pip install flask
```
3. View installed libraries
```
(virt) ~/Flask-Elastic-Beanstalk$ pip freeze
```
4. Save the output from freeze to a requriements.txt file for elastic beanstalk to use
```
(virt) ~/Flask-Elastic-Beanstalk$ pip freeze > requirements.txt
```

### 3. Install, run, and test the Flask App
```
(virt) ~/Flask-Elastic-Beanstalk$ make all
pip install --upgrade pip &&\
        pip install -r requirements.txt
Requirement already satisfied: pip in ./virt/lib/python3.9/site-packages (24.0)
...
Requirement already satisfied: zipp==3.17.0 in ./virt/lib/python3.9/site-packages (from -r requirements.txt (line 9)) (3.17.0)
pylint --disable=R,C application.py

--------------------------------------------------------------------
Your code has been rated at 10.00/10 (previous run: 10.00/10, +0.00)


(virt) ~/Flask-Elastic-Beanstalk$ 
 * Serving Flask app 'application'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on http://127.0.0.1:5000
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 417-347-959
```
Open another terminal tab
```
(virt) ~/Flask-Elastic-Beanstalk$ curl http://127.0.0.1:5000/
Continuous Delivery Demo

(virt) ~/Flask-Elastic-Beanstalk$ curl http://127.0.0.1:5000/echo/My-Name
{
  "new-name": "My-Name"
}
```
close the new tab

Deploy the site with EB CLI

First make a .ebignore file to ignore the virtual environment
```
(virt) ~/Flask-Elastic-Beanstalk$ touch .ebignore
(virt) ~/Flask-Elastic-Beanstalk$ vim .ebignore
```
add 'vert' to the .ebignore file.

Initialize the EB CLI repository with eb init
```
(virt) ~/Flask-Elastic-Beanstalk$ eb init -p python-3.7 flask-tutorial --region us-east-1
Application flask-tutorial has been created.
```

Create an environment and deploy the application with eb create:
```
(virt) ~/Flask-Elastic-Beanstalk$ eb create flask-env
```

Will take about 5 minutes for AWS to standup and launch the app.
