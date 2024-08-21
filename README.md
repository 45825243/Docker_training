# Working with Docker
## Steps
1. #### Connect to github 
``` 
git init
git remote add origin https://github.com/45825243/Docker_training.git
git add .
git commit -m "changes"
git push origin master 
``` 
we make sure we have connection to our git repo.

2. #### Create venv with command 
```
python -m venv venv
```
After that to activate our venv we need to give access for this environment
```
Set-ExecutionPolicy RemoteSigned -Scope Process
```
Now we can activate our venv
```
venv\Scripts\Activate.ps1
```
Now we are in our virtual environment and it's look like this

![venv](images\2024-08-20_16-00-18.png)

3. #### Install required packages and set up our project
```
pip install flask
```
After installing Flask, freeze the installed packages into `requirements.txt` by running `pip freeze > requirements.txt`.
Now we need to create a new folder called **web-app**, go into this folder, create thi file **app.py**, for this we use steps: 
``` 
mkdir web-app
cd web-app
type nul > app.py
```
We created a file in the **web-app** folder called **app.py** and now we need to paste code onto this file. Use command 
```
code app.py
```
to open the file and paste the code inside
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
```
now we test our file with
```
python app.py
```
Your command line give you a choice which link to open

![app.py](images\run_code.png)

After you open the link you can see browser and "Hello, World!". It means your code is working. Click CTRL+C to go back to venv
But we need to run the same from the Docker container.

4. #### Docker
In the same folder create **Dockerfile** and open it.
```
type nul > Dockerfile
```
Paste the code
```
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```
Run the command `docker build .` And don't forget to run docker desktop before this
