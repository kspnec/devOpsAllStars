# Create your project structure.

src - directly hold all of our main code.
tests - for unit tests, important for devops practices.
data - local storage for developement testing.

src/__init__.py  - makes our directory a python package. This allows imports between different files.
requirements.txt - everything that is required to run this project.

README.md  - gives general overview about what this project is about.

### Next, Initialize git to track your project using VCS.
git init
git branch -M main

echo ".env" >> .gitignore
.gitignore - basically tells the project what to ignore, What not to track.
.env - you never commit your access keys or any secrets or private keys for security.

### Python actually creates these, but we don't have to track them.
echo "__pycache__/" >> .gitignore
echo "*.zip" >> .gitignore

### Requirements.txt - shopping list for our projects.
echo "boto3==1.26.137" >> requirements.txt 
echo "python-dotenv==1.0.0" >> requirements.txt 
echo "requests==2.28.2" >> requirements.txt 

boto3 is aws sdk for python, it basically allows us to talk to AWS.
python-dotenv - manages out env variables 
requests - we can make HTTP request to the wheather API - https://home.openweathermap.org/api

All the package version numbers - ensures that we have consistent environments.

### create pyhton virtual environment 
python3 -m venv .venv 
echo ".venv" >> .gitignore

.venv - for dependency isolation and consistency across environments., etc 

source .venv/bin/activate
// upgrade pip version to latest for the python virtual env.
.venv/bin/python3 -m pip install --upgrade pip
// install python packages
pip install -r requirements.txt


### Next, Move on to our environment setup Instructions.
Configure AWS CLI creds
Holds credentials and our access keys from open wheater api website.

export AWS_PROFILE=kk-temp-user
aws configure
aws configure list


echo "OPENWEATHER_API_KEY=your_openweather_api_key" >> .env
// Bucket name must be globally uniqe
echo "AWS_BUCKET_NAME=weather-dashboard-${RANDOM}" >> .env

src/weather_dashboard.py - python script, the main logics for this application.


### Run the script now.

## Read a json file from s3 bucket.
aws s3api get-object --bucket weather-dashboard-19xxx --key "weather-data/New York-20250206-195959.json" /dev/stdout | jq .

## Read multiple files from s3 bucket.
aws s3 ls s3://weather-dashboard-19722/weather-data/ | awk '{print $4}' | while read file; do
  aws s3api get-object --bucket weather-dashboard-19722 --key "weather-data/$file" /dev/stdout
done