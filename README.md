# streaming-04-multiple-consumers
### Student: Luci McDaniel
### May 24, 2024
### GitHub Profile: https://github.com/LuciMcD 


> Use RabbitMQ to distribute tasks to multiple workers

One process will create task messages. Multiple worker processes will share the work. 


## Before You Begin

1. Fork this starter repo into your GitHub.
1. Clone your repo down to your machine.
1. View / Command Palette - then Python: Select Interpreter
1. Select your conda environment. 

## Read

1. Read the [RabbitMQ Tutorial - Work Queues](https://www.rabbitmq.com/tutorials/tutorial-two-python.html)
1. Read the code and comments in this repo.

## RabbitMQ Admin 

RabbitMQ comes with an admin panel. When you run the task emitter, reply y to open it. 

(Python makes it easy to open a web page - see the code to learn how.)

## Execute the Producer

1. Run emitter_of_tasks.py (say y to monitor RabbitMQ queues)

Explore the RabbitMQ website.
Note: Make sure module pika is installed. Open a new terminal and use command for Windows: python -m pip install pika. 

## Execute a Consumer / Worker

1. Run listening_worker.py

Will it terminate on its own? How do you know? 
This will not terminate on its own. Ctrl C, is required to stop the process. It will continue to wait for another message. 

## Ready for Work

1. Use your emitter_of_tasks to produce more task messages.

## Start Another Listening Worker 

1. Use your listening_worker.py script to launch a second worker. 

Follow the tutorial. 
Add multiple tasks (e.g. First message, Second message, etc.)
How are tasks distributed? Tasks are split between the 2 workers. While the first worker is waiting the second worker receives the second message. Each worker receives every other message. 

Monitor the windows with at least two workers. 
Which worker gets which tasks? The first terminal opened, or the first worker receives the first message and the next terminal will receive the next message and so on. 

## Creating v3_emitter_of_tasks.py and v3_listening_worker.py
The code for both scripts was initially copied from v2 and then edited. 
Edits made were: 
ADD:
    import csv
    import time

    from util_logger import setup_logger
    logger, logname = setup_logger(__file__)

     with open('tasks.csv', 'r') as file:
            reader = csv.reader(file)
            for row in reader:
                task = ''.join(row)

REMOVE:
    message: str parameter from the function and from the bottom of the script when the function is called. 

CHANGE:
    message was changed to task
    task_queue was changed to task_queue3



## Reference

- [RabbitMQ Tutorial - Work Queues](https://www.rabbitmq.com/tutorials/tutorial-two-python.html)


## Screenshot

See a running example with at least 3 concurrent process windows here:
This image shows how the messages are distributed, before using logging instead of print statements.
![alt text](image.png)

Screenshot after adding logging.
![alt text](image-1.png)

Screenshot of version3 running.
![alt text](image-2.png)
