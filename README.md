# Hands-on Lab: Deploy Your Django App on IBM Cloud Foundry
Learning Objectives
Understand how to prepare your Django app for Cloud Foundry Deployment
Deploy your app on IBM Cloud Foundry
Pre-requisites
You will need an IBM Cloud account to do this lab.

# run these following command in terminal :

$ ibmcloud login -u youremail -p yourpassword

$ ibmcloud cf install

$ ibmcloud target -o yourorg -s yourspace

$ ibmcloud cf domains

# prepare app and database
# get the template ready for deployment
wget "#link to download project" or git clone 'HTTP' or open project from local
unzip 'file-name.zip'
rm 'file-name.zip'

# run commnad:
$ibmcloud cf domains
$pip3 install -r requirements.txt
(you maybe need to update dependensies like $ pip install --upgrade pip )

# perform and run migration
$ python3 manage.py makemigrations
$ python3 manage.py migrate
$ python3 manage.py runserver

# Launch Application with port 8000
# add the /onlinecourse path and your full URL 

# Deploying a Django App on IBM Cloud Foundry
# prepare the gunicorn server for Django app
# To serve those static files, we will need another webserver for better load balancing management. Cloud Foundry provides a Staticfile buildpack supported by nginx server

# create empty file "procfile" under project root folder and add this command

web: gunicorn myproject.wsgi

# create manifest.yml file to cuztomize IBM cloud

applications:
  - name: onlinecourse  <*app name>
    routes:
      - route: yourhost.us-south.cf.appdomain.cloud  <*hostname.domainname>
    memory: 128M
    buildpack: python_buildpack
  - name: onlinecourse-nginx <*app name.static server>
    routes:
      - route: yourhost.us-south.cf.appdomain.cloud/static <*hostname.domainname>
    memory: 128M
    buildpack: staticfile_buildpack

# Find ALLOWED_HOSTS list in myproject/settings.py and append the host using the route entry in manifest.yml

ALLOWED_HOSTS = ['yourhostname.domainname']

# start deploying  django online app

$ ibmcloud cf push

# wait until deployment are finished

Waiting for app to start...

# then viit url in the app you have just pushed on cloud foundry
# click the Visit App URL link and add a /onlinecourse path. Your full URL
sample url : yluo.us-south.cf.appdomain.cloud/onlinecourse
You may also try to access a static file such as
yluo.us-south.cf.appdomain.cloud/onlinecourse/static/media/course_images/django.png 
# which is servered by onlinecourse-nginx app.

# In this lab, you have learned how to prepare and deploy the onlinecourse app on IBM Cloud Foundry. In addition, you have learned that to start a ngix server to serve the static files of your onlinecourse app on IBM Cloud Foundry.