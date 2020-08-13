# How to use notebooks
source: https://jupyter-docker-stacks.readthedocs.io/en/latest/index.html

### Compose
`docker-compose up --build` DONT use -d flag because you need to get the notebook server token from the output.
`docker exec -it notebookserver bash`
`docker exec -it -u 0 notebookserver bash` to run container as root

### Flask
This is just for simple dev work. For production ready flask use the flask docker project.
From inside the container: `docker exec -it notebookserver bash` run
`flask run --host=0.0.0.0` this will run flask with the env var: flask/flask_app.py as specified in Dockerfile.
To run another flask file put it in the shared volume (in the "flask" folder) and open the container like this with a new env var:
`docker exec -it -e FLASK_APP="flask/flask_app2.py" notebookserver bash` and
`flask run --host=0.0.0.0`


### Development with VSCode inside the container context
- Needed Extensions:
  - Python
  - Python for VSCode
  - Docker
  - Remote-Containers
  - (Material Icon Theme)

- `ctrl + shift + p` -> Remote-Containers: Open folder in container... -> choose the docker-compose.yml containing folder
  - see: https://code.visualstudio.com/docs/remote/containers#_creating-a-devcontainerjson-file
- Choose python interpreter (from the python installed in the container) at the status line left side
-
### Mysql server
- docker-compose starts a mysql8 server instance that can be connected to with db:3306 (or just: db) 
- the start script in mysql/mysql_script/pythondemo.sql is copied into the contaier and executed at startup
- user root:root and dev:ax2 (with only grants on database: db)
- `docker exec -it mysql_notebooks bash` and `mysql -u root -proot`
- docker restart <container id>` to restart the mysql server
### Flask server


### clean up
- `docker rmi $(docker images -f "dangling=true" -q)` to remove all intermediate images to save disk space.
or use `--force-rm` with docker-compose build to auto remove them right after build is done.

### If not using compose:
- If not allready done: `docker pull jupyter/scipy-notebook:ubuntu-18.04`  
- run container with volume: `docker run -p 8888:8888 -v $PWD:/home/jovyan/work jupyter/scipy-notebook:ubuntu-18.04`  
- access container from cli: `docker exec -it container_id_here bash`  

### Course content

There will be weekly handin assignments and that is how you get studypoints (no points are given for attendance!)
Throughout the semester you must have **10 approved handins** to qualify for examination.

Preliminary Class schedule is shown below (subject to change)

|Week|Time|Topic|Hand-in|
|--|--|--|--|
|Week 35<br/>24-08-2020|Monday 9:00-12:30 ROOM 1.05|Getting started, Python language features|[Ex 1](notebooks/01-Exercise.ipynb)|
|Week 36<br/>31-08-2020|Monday 9:00-12.30 on ZOOM|Whirlwind, Lists, Loops, Cond. Stmts., Functions, Modules|[Ex 2](notebooks/02-Exercise.ipynb)|
|Week 37<br/>|TBD|OO, Exceptions, plotting|[Ex 3](notebooks/03-Exercise.ipynb)|
|Week 38<br/>|TBD|Intro to Numpy|[Ex 4](notebooks/04-Exercise.ipynb)|
|Week 39<br/>|TBD|Intro to Pandas|[Ex 5](notebooks/05-Exercise.ipynb)|
|Week 10<br/>|TBD|Multiprocessing, generators and intro to Requests|[Ex 6](notebooks/06-Exercise.ipynb)|
|Week 41<br/>|TBD|Webscraping Basics, Regular Expr. & Selenium|[Ex 7](https://docs.google.com/document/d/1ojSiBWwLo4-Rc7763vx6aVEYdNluATOMja9qqk4dodU/edit?usp=sharing)|
|Week 42<br/>|Efterårsferie|
|Week 43<br/>|TBD|Database and web service|[](https://docs.google.com/spreadsheets/d/10HYM2KRqslBTQjkcz8B0ooz4TnnXd4n5xxFsSl9saZQ/edit#gid=0)|
|Week 44<br/>|TBD|Graphs & PageRank Algorithm|[](notebooks/Facebook_exercise.ipynb)|
|Week 45<br/>|TBD|Feature spaces|[](notebooks/Ugeopgave-10.ipynb)|
|Week 46<br/>|TBD|Neural Networks|[](notebooks/11-1-Exercise-Perceptrons.ipynb)|
|Week 47<br/>|TBD|Image Processing with OpenCV||
|Week 48<br/>|TBD|Movement Detection||
|Week 49<br/>|TBD|Exam Project period|None|
|Week 50<br/>|TBD|Exam Project period|None|
|Week 51<br/>|TBD|Exam Project period|None|
|Week 51<br/>|Fredag 23:59|Handin exam project|Exam project|  


