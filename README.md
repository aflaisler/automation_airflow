# General reports automation - Airflow's dags (directed acyclic graph)

# General description

For this automation project, we decided to use Apache Airflow to programmatically
 author, schedule and monitor workflows. Airflow is very similar to other automation
 servers like Jenkins except it is written in pure Python. Another difference is
 that Airflow uses directed acyclic graphs (dags) to define workflows of tasks.

 We are going to go through how the graphs are defined in this project.


 # The files

------
dags
------

dag-dotcom-xxxxx-weekly.py

DESCRIPTION:
Airflow's dag are extremely simple to program: each file represent one pipeline.
Each file contains tasks (~ 4) which have a specific order.
For this project we are going to use only BashOperator tasks from airflow.
BashOperator is a type of airflow's tasks. It will execute the bash command that you
pass as argument.

Airflow's dag need to follow this structure:
1) Define your graph using airflow's DAG module (this is where you assign the name
  and the parameters for the tasks (schedule, retry_delay, description, etc.))

2) Write the different tasks that will need to be run in the pipeline

3) Set the order of the tasks

USAGE:
Once you have written the graph (following the 3 steps we described above), then
you need to put the file in the airflow directory in the folder dags.
Airflow will automatically pick it up.

A good practice is to test the task to make sure it runs without errors. To do
that, run the following:
airflow list_dags => will  return a list of the graphs

select the pipeline you just defined and do:
airflow list_tasks <name of your graph> => you should all the tasks you defined in
your dag.

Now we need to test them one by one. Do:
airflow test <name of your graph> <task1> <date>
(notice you have to give a date as an argument. When testing I usually use 2018-1-1).

=> You should now see your task being executed by airflow with some verbosity.
If everything works fine you should get an error code 0.

Next repeat the testing with the other tasks. Once they all pass you are ready to
schedule the workflow. Run:
airflow scheduler -D & airflow webserver -p 8080

In your browser go to: http://localhost:8080
=> turn on your pipeline.

For more information regarding the DAGs or the scripts please contact me: aflaisler at gmail.com
