Task 1 1- Explain how the application works? Write a short paragraph about the framework.

Firstly, we have to connect to OpenStack API environment by using the Runtime Configuration (RC) file. Then we can contextualize our production server based on CloudInit configuration file and OpenStack python code. Once the contextualization process finished, we can see our production server and access the webpage. Secondly, we start a request through Flask which based a frontend web server. The server passes the request to the Celery and RabbitMQ backend server, the running worker node developed with Keras and TensorFlow will run the prediction models and send back results. Finally, frontend server will show us the predicting results.

2- What are the drawbacks of the contextualization strategy adopted in the task-1? Write at least four drawbacks.

It will take very long time to run the model on the backend server, since we only have one worker node.

if we want to horizontally scale the application, we have to manually set all the things again. If one server failed, our whole system will stop working, we don't have any backup servers. If we want to update the database, we have to get access into the database and do it manually. It's not dynamic system.

There are only one frontend and one backend, it cannot handle more requests.

3- Currently, the contextualization process takes 10 to 15 minutes. How can we reduce the deployment time?n we can use docker containers to reduce the contextualization processing time. Right now we just use one virtual machine to run our application, but we can use docker containers to start our application into different components.

4- Write half a page summary about the task and add screenshots if needed.
![image](https://github.com/comeasure/DataEngineering/assets/71668932/3afd2b9e-af8e-4185-92be-4019951e79a3)


what This task is a machine learning model-as-a-service application based on a web server. We start a client node first to contextualize the whole system including frontend server, backend server and model execution environment. We use Flask to set web application with a app.py file which contained, Celery and RabbitMQ for the backend server, Model execution environment based on Keras and TensorFlow. Flask depends on the Jinja template engine and the Werkzeug WSGI toolkit, we use "POST" and "GET" motheds to pass the messages from costumer to the server. Then we use Celery and RabbitMQ to communicate between backend node and worker node via messages. To initiate a task the backend adds a message to the queue, the broker then delivers that message to a worker. In our worker node, we execute our prediction task by loading data and model from pima-indiansdiabetes.csv file and model.jason file. After the execution, the worker will send back the message to backend by Celery and RabbitMQ, then then backend server will send back the results to frontend server by Flask. The result including "Accuracy", "True data array" and "Predicted array" will show to customer on the web page. Questions

1- What problems Task-2 deployment strategy solves compared to the strategy adopted in Task-1?

In Task 1, we only have one vitrual machine which contains everything inside. That means we cannot scale this kind of environment. In task 2, we use docker containers to containerize every components of our application, then we can scale the environment.

2- What are the outstanding issues that the deployment strategy of Task-2 cannot not address?

If we want to change something in our model or put some new data in to the model, the system of task 2 cannot do it automatically.

3- What are the possible solutions to address those outstanding issues?

If we use Githooks to build an execution pipelines, it will provide us continuous integration and delivery to our production server. 4- What is the difference between horizontal and vertical scalability? Is the strategy adopted in Task-2 follow horizontal or vertical scalability?

For vertical scalability, we scale the abilities of one single node, such as deployed more CPU ability to it. For horizontal scalability, we scale more nodes to execute the tasks at the same time. The strategy in Task 2, it follows the horizontal scalability, we containerize more work nodes to solve the task.

5- Write half a page summary about the task and add screenshots if needed.
![image](https://github.com/comeasure/DataEngineering/assets/71668932/881068ad-5bd8-462d-91cb-82dc6dd74bb7)


Depends on same application structure of task 1. In task 2, instead of building all the stuffs of our application in a single virtual machine, we use docker compose to deploy every components of the application. In the dockerfile, we only asked it to read a requirements.txt file which contains all the names of packages we needed, then we can install them simultaneously. It helps us to reduce the time of contextualization process compared with Task1. In the docker-compose.yml, we set our web configuration and the connections between backend server and worker nodes by Celery and RabbitMQ. It also means we can horizontally scale our cluster by the command "docker-compose up -- scale worker_1=3 -d" if we needed. Questions 1 - What is the difference between CloudInit and Ansible?

CouldInit is a multi-distribution package that handles early initialization of a cloud instance. Ansible is a radically simple IT automation platform that makes your applications and systems easier to deploy and maintain. Automate everything from code deployment to network configuration to cloud management, in a yaml file with simple lauguage, using SSH, with no agents to install on remote systems. In our Ansible playbook, the configuration variables used in deploying prod_server and dev_server environment can be retrieved later by using the setup_vars.yml set of tasks.

2 - Explain the configurations available in dev-cloud-cfg.txt and prod-cloud-cfg.txt files. It's several txt files including user name, sudo privileges, home path, shell path and ssh authorized key for our production server and devolopment server initial environment.

3 - What problem we have solved by using Ansible?

The most important solution that Absible offered is to help devolopers managing plenty of servers deployed or update at same time. Sometime we will have multiple sequential or repetitive tasks to deploy, Ansible helps us to do configuation, installation and deployment steps in a single YAML file. if we do it manully, it will comsume a lot of time even including mistakes by humans. We can re-use same file mutiple times and for different environment. Ansible also let us excute tasks from our own machine, we don't need to ssh into all remote servers. Ansible is agentless, that means we don't need to install a agent into any server, it can save our deployed time. Also Ansible is absolutely more efficient and reliable.
![image](https://github.com/comeasure/DataEngineering/assets/71668932/59d037b3-467d-4440-9570-2541fa5eba95)

