1.create jupyter configure file:
	jupyter notebook --generate-config
2.append configure into configure file:
	c.NotebookApp.ip = ''	# ip
	c.NotebookApp.open_browser = False
	c.NotebookApp.password = 	# see next
	c.NotebookApp.port = 8889
	c.NotebookApp.notebook_dir = ''	# notebook save path
	c.NotebookApp.allow_remote_access = True
2.2 create password:
	python
	>>> from notebook.auth import passwd
	>>> passwd()