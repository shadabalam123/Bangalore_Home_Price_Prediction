# Bangalore_Home_Price_Prediction
This Project covers Real_estate_price prediction model along with deployment of the model on the AWS EC2 instance.
Following are the steps i followed to build a Price Prediction Website

1.Imported the Data set from the Kaggle.com

2.Build the model using sklearn. Selected LinearRegression as the best model using GridSearchCV.

 > Technology and Tools covered to build this model are:-
 
    a. Python
    b. Numpy and Pandas for Data Cleaning. This part covers dropping data, outlier removal, feature engeineering, dimensionality reduction.
    c. Matplotlib for Data Visualization.
    d. GridSearchCV for Hyperparamater Tuning 
    e. KFold Cross validation
    d. sklearn for model building.

3.Built the website using HTML,CSS,Java Script ,allowing the user to enter BHK,Bath,Squarefeet and e.t.c. as the input from the user .

4.Build the framework of the server using Flask to get the response in the form of predicted price on getting the requests from the client.Created the endpoint of the ui as get_location_names and predict_home_price.



# Deployment Process in AWS EC2 instance

1. Created EC2 instance using AWS console 
2. Now connected with the EC2 instance using the below command on the Gitbash 
- $  ssh -i "C:\Users\shada\.ssh\BHPP.pem" ubuntu@ec2-52-15-179-105.us-east-2.compute.amazonaws.com
3. Installed  nginx on EC2 instance using the below command
- sudo apt-get update
- sudo apt-get install nginx
4. Load the cloud url on the browser . On loading we will see "Welcome to nginx". This means our nginx server is running on the browser
5. Connected the EC2 instance with the winscp tool. Once we are connected we are at /home/ubuntu/ folder. Now i copied  all the files to /home/ubuntu/ folder.Finally my path becomes:- /home/ubuntu/pythonProject123
6. Now i created this file-  /etc/nginx/sites-available/bhp.conf by changing the default setup in order to route the request to this url http://127.0.0.1:5000.
7. Here is the bhp.conf file
 
server {
 
	  listen 80; 
    
	server_name bhp;

	root /home/ubuntu/pythonProject123/client;
	index app.html;

	location /api/ {
		rewrite ^/api(.*) $1 break;
		proxy_pass http://127.0.0.1:5000;
	}
}

8. Create symlink for this file in /etc/nginx/sites-enabled by running this command
- sudo ln -v -s /etc/nginx/sites-available/bhp.conf
9. Remove symlink for default file in /etc/nginx/sites-enabled directory
- sudo unlink default
10. Restart nginx
- sudo service nginx restart
11. Finally installing python packages and start flask server by running the below command
- sudo apt-get install python3-pip.
- sudo pip3 install -r /home/ubuntu/pythonProject123/server/requirements.txt
- python3 server.py
12. Finally it will run the server on 5000 port. Lastly loaded my cloud url i.e. http://ec2-52-15-179-105.us-east-2.compute.amazonaws.com/ to the web browser. Now it is ready in the production cloud environment.

