### Boston House Pricing Prediction

### Softwares and tools requirements

1. [Github Account](https://github.com)
2. [Heroku Account](https://heroku.com)
3. [VS Code IDE](https://code.visualstudio.com)
4. [Git CLI](https://git-scm.com/book/en/v2/Getting-Started-The-Command-Line)

Create a new environment
```
conda create -p venv python==3.7 -y
```
## Setting up Git
Connected with github repository. From now, changes are made with 
```
git add
git status
git commit -m "Commit message"
git push origin main
 ```




## Creating A FLASK Web Application
Created app.py to: make a Flask app, load the pickled model, define methods for the routes.
Create a home.html page with "hello world".
```
<h1>
"hello world"
</h1>
```



# Run app.py with localhost
```
python app.py
```
Open http://127.0.0.1:5000 on browser. Right now, it just shows "hello world".



# Running An Testing our application with Postman
In Postman, create a body with json (key:value of 13 house factors) that we will POST to the api address (http://127.0.0.1:5000/predict_api) to receive new prediction. 

When we hit "Send", Postman sends the json data to the post address (route ".../predict_api"), which calls app.py to execute predict_api() function, and return a price prediction.


# Create Front End Application to receive direct user inputs, instead of through Postman
Make a form with home.html, so 127.0.0.1:5000 can accept 13 house price factors from user inputs, and a button "Predict". 
```
<form action="{{ url_for('predict')}}"method="post">
...
<button type="submit" class="btn btn-primary btn-block btn-large">Predict</button>
```

When we hit "Predict", we go into route "127.0.0.1:5000/predict", which calls app.py to excecute predict() function, and return a price prediction.

Application returns the prediction, e.g. "The predicted house price is 20.734120566346643"


# Procfile for Heroku Deployment
Created Procfile.
```
web: gunicorn app:app
```

# Deploying The App To Heroku

Created Heroku account, created new application, and set deployment from github repository.

Application was sucessfully built but cannot be displayed. Heroku has cancelled free plan.



# Deploying The App Using Dockers
Created Dockerfile

```
FROM python:3.7
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
EXPOSE $PORT
CMD gunicorn --workers=4 --bind 0.0.0.0:$PORT app:app
```
Created .github\workflows\main.yaml to deploy containerized app from Heroku.
In github secret actions, create new secrets holding information of Heroku account (api keys, app name, email).


When pushed to github, errors are:
```
build
Building container failed. Error: undefined

Node.js 12 actions are deprecated. For more information see: https://github.blog/changelog/2022-09-22-github-actions-all-actions-will-begin-running-on-node16-instead-of-node12/. Please update the following actions to use Node.js 16: actions/checkout, gonuit/heroku-docker-deploy, actions/checkout

```