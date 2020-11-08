---
layout: post
title: Asynchronous Tasks With Django and Huey
---


I was working on a project and to achieve some results I wanted it to run some background process. It has to run outside the request-response cycle of request. When it comes to run async code in python, we generally use a task queue to achieve it. 

[Celery](https://docs.celeryproject.org/en/stable/) is the mostly used in the community and I've been already using it on other projects at work. But task was to run a simple task and also I was on some resource constraints this time and Celery was obviously an overkill here. I found [Huey](https://github.com/coleifer/huey), a lightweight and simple task queue for python and it integrates well with Django.

Huey supports following as backend storage:

 - Redis
 - SQLite
 - In Memory
 - File System

Default storage engine used is Redis, but in my case I was not using any redis server and as I said before there are some resource constraints so running a new redis server is not an option here. So, I preferred to use SQLite storage.

The configuration is pretty simple here.

 - **Install package:**		

```python
    	pip install huey
```

 - **Add config in settings.py**

```python
	# HUEY Configuration https://huey.readthedocs.io/en/latest/django.html  
	HUEY = {  
	'huey_class': 'huey.SqliteHuey', # Huey implementation to use.  
	'name': 'app.huey', # Use db name for huey.  
	'results': True, # Store return values of tasks.  
	'store_none': False, # If a task returns None, do not save to results.  
	'immediate': False, # If DEBUG=True, run synchronously.  
	'utc': True, # Use UTC for all times internally.  
	'consumer': {  
		'workers': 1,  
		'worker_type': 'thread',  
		'initial_delay': 0.1, # Smallest polling interval.
		'backoff': 1.15, # Exponential backoff using this rate.
		'max_delay': 10.0, # Max possible polling interval.  
		'scheduler_interval': 1, # Check schedule every second.
		'periodic': True, # Enable crontab feature.
		'check_worker_health': True, # Enable worker health checks.
		'health_check_interval': 1, # Check worker health every second.
	},  
	}

```

 - **Run consumer process:**  Run a consumer process in another tab or using supervisor:

```bash
	> Running locally: 

		python manage.py run_huey

	> Using supervisor:

	    [program:huey]
		directory=/home/ubuntu/matrim-backend
		command=/path/to/env/bin/python manage.py run_huey
		autostart=true
		autorestart=true
		stderr_logfile=/var/log/huey.err.log
		stdout_logfile=/var/log/huey.out.log


```

 - **Code changes:** There are no significant code level changes you need to perform to run task asynchronously now.

```python

# file: webapp/services.py
from huey.contrib.djhuey import task

@task()  
def run_processing_service(document_id):  
    logger.info(f"started process: {document_id}")
    # run your code as you were running it before.


# file: webapp/views.py

def home(request):
	# your code here
	run_processing_service(document.id)
	# your code here
	return response

```


That's all you need to run your code asynchronously.

