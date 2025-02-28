# kodekloud free labs linux final troubleshooting scenario

Success doesn’t come to you, you go to it.

– Marva Collins

## 1 / 17

Bob needs your help to get his app ready in time for the client presentation!
His app is working perfectly on his own laptop, but while transferring the code to the Dev servers, things are not working as expected!
Wherever required, use sudo to run commands as the root user. Bob's password is caleston123.
Proceed to the next question to see the application architecture.

## 2 / 17

Here is the simple architecture diagram of the implementation. This is a two-tier application.

The web server is hosted on devapp01.
The DB server is hosted on devdb01
Bob has done his bit when it comes to the code. Everything is set up to work properly.
All you need to do is to fix some of the things he has missed while migrating the code and the database on the DEV servers.
Click on OK to move to the first task.

(там на схеме нарисована машина с БД постгре и вебсервером и что есть сетевой досутп с машины на которой ты работаешь)

## 3 / 17 

Task 1:
Copy the file caleston-code.tar.gz from Bob's laptop to Bob's home directory on the webserver devapp01
Bob's password is caleston123

```
bob@caleston-lp10:~$ scp caleston-code.tar.gz bob@devapp01:/home/bob
bob@devapp01's password: 
caleston-code.tar.gz
```

## 4 / 17

Task 2:
On the devapp01 webserver, unzip and extract the copied file in the directory /opt/.
The password for the devapp01 webserver is caleston123.

```
bob@devapp01:~$ sudo tar -xzf caleston-code.tar.gz -C /opt/
[sudo] password for bob: 
bob@devapp01:~$ ls -la /opt/
total 16
drwxr-xr-x 1 root root 4096 Feb 28 10:35 .
drwxr-xr-x 1 root root 4096 Feb 28 10:28 ..
drwxrwxr-x 6 bob  bob  4096 Jan  8  2021 caleston-code
```

## 5 / 17
Task 3:
Delete the tar file from devapp01 webserver.

```
bob@devapp01:~$ rm -rf caleston-code.tar.gz
```

## 6 / 17

Task 4:
Make sure that the directory is extracted in such a way that the path /opt/caleston-code/mercuryProject/ exists on the webserver.

```
bob@devapp01:~$ ls -la /opt/caleston-code/mercuryProject/
total 60
drwxrwxr-x 7 bob bob  4096 Jan  8  2021 .
drwxrwxr-x 6 bob bob  4096 Jan  8  2021 ..
-rw-rw-r-- 1 bob bob  1997 Jan  8  2021 .gitignore
-rw-rw-r-- 1 bob bob  7079 Jan  8  2021 admin.json
drwxrwxr-x 3 bob bob  4096 Jan  8  2021 blog
-rw-rw-r-- 1 bob bob 15331 Jan  8  2021 db.json
-rwxrwxr-x 1 bob bob   627 Jan  8  2021 manage.py
drwxrwxr-x 3 bob bob  4096 Jan  8  2021 media
drwxrwxr-x 2 bob bob  4096 Jan  8  2021 mercury
drwxrwxr-x 3 bob bob  4096 Jan  8  2021 portfolios
drwxrwxr-x 3 bob bob  4096 Jan  8  2021 templates
```

## 7 / 17

For the client demo, Bob has installed a postgres database in devdb01.
SSH to the database devdb01 and check the status of the postgresql.service
What is the state of the DB?
Bob's password is caleston123

ssh to devdb01 with bob username and password:
```
bob@devdb01:~$ systemctl status postgresql.service
● postgresql.service - PostgreSQL RDBMS
   Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: enabled)
   Active: inactive (dead) since Fri 2025-02-28 10:29:12 UTC; 9min ago
  Process: 5327 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
 Main PID: 5327 (code=exited, status=0/SUCCESS)
```

right answer - inactive(dead)

## 8 / 17

Task 5:
Add an entry host  all  all 0.0.0.0/0 md5 to the end of the file /etc/postgresql/10/main/pg_hba.conf on the DB server.
This will allow the web application to connect to the DB.

```
bob@devdb01:~$ echo "host  all  all 0.0.0.0/0 md5" | sudo tee -a /etc/postgresql/10/main/pg_hba.conf
host  all  all 0.0.0.0/0 md5
bob@devdb01:~$ sudo tail /etc/postgresql/10/main/pg_hba.conf 
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
# IPv6 local connections:
host    all             all             ::1/128                 md5
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     peer
host    replication     all             127.0.0.1/32            md5
host    replication     all             ::1/128                 md5
host  all  all 0.0.0.0/0 md5
```

## 9 / 17

Task 6:
Start the postgres DB on the devdb01 server.

```
bob@devdb01:~$ sudo systemctl enable --now postgres
Failed to enable unit: Unit file postgres.service does not exist.
bob@devdb01:~$ sudo systemctl enable --now postgresql
Synchronizing state of postgresql.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable postgresql
bob@devdb01:~$ systemctl status postgresql
● postgresql.service - PostgreSQL RDBMS
   Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: enabled)
   Active: active (exited) since Fri 2025-02-28 10:45:21 UTC; 9s ago
  Process: 6085 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
 Main PID: 6085 (code=exited, status=0/SUCCESS)
bob@devdb01:~$ netstat -ntlp | grep 5432
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
tcp        0      0 0.0.0.0:5432            0.0.0.0:*               LISTEN      -                   
tcp6       0      0 :::5432                 :::*                    LISTEN      -
```

## 10 / 17

What port is postgres running on? Check using the netstat command?
Bob's password is caleston123.

right answer - 5432

## 11 / 17

Task 7:
Back on the devapp01 webserver. Attempt to start the web application by:
Navigate to the directory /opt/caleston-code/mercuryProject
Next, run the command python3 manage.py runserver 0.0.0.0:8000
Was the command successful? Did the application load up?
Key in Control + C to get back to the bash prompt.

```
bob@devapp01:/opt/caleston-code/mercuryProject$ python3 manage.py runserver 0.0.0.0:8000
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
Exception in thread django-main-thread:
Traceback (most recent call last):
  File "/usr/local/lib/python3.6/dist-packages/django/db/backends/base/base.py", line 217, in ensure_connection
    self.connect()
  File "/usr/local/lib/python3.6/dist-packages/django/db/backends/base/base.py", line 195, in connect
    self.connection = self.get_new_connection(conn_params)
  File "/usr/local/lib/python3.6/dist-packages/django/db/backends/postgresql/base.py", line 178, in get_new_connection
    connection = Database.connect(**conn_params)
  File "/usr/local/lib/python3.6/dist-packages/psycopg2/__init__.py", line 127, in connect
    conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
psycopg2.OperationalError: could not connect to server: Connection refused
        Is the server running on host "localhost" (127.0.0.1) and accepting
        TCP/IP connections on port 5433?
could not connect to server: Cannot assign requested address
        Is the server running on host "localhost" (::1) and accepting
        TCP/IP connections on port 5433?


The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "/usr/lib/python3.6/threading.py", line 916, in _bootstrap_inner
    self.run()
  File "/usr/lib/python3.6/threading.py", line 864, in run
    self._target(*self._args, **self._kwargs)
  File "/usr/local/lib/python3.6/dist-packages/django/utils/autoreload.py", line 54, in wrapper
    fn(*args, **kwargs)
  File "/usr/local/lib/python3.6/dist-packages/django/core/management/commands/runserver.py", line 120, in inner_run
    self.check_migrations()
  File "/usr/local/lib/python3.6/dist-packages/django/core/management/base.py", line 453, in check_migrations
    executor = MigrationExecutor(connections[DEFAULT_DB_ALIAS])
  File "/usr/local/lib/python3.6/dist-packages/django/db/migrations/executor.py", line 18, in __init__
    self.loader = MigrationLoader(self.connection)
  File "/usr/local/lib/python3.6/dist-packages/django/db/migrations/loader.py", line 49, in __init__
    self.build_graph()
  File "/usr/local/lib/python3.6/dist-packages/django/db/migrations/loader.py", line 212, in build_graph
    self.applied_migrations = recorder.applied_migrations()
  File "/usr/local/lib/python3.6/dist-packages/django/db/migrations/recorder.py", line 73, in applied_migrations
    if self.has_table():
  File "/usr/local/lib/python3.6/dist-packages/django/db/migrations/recorder.py", line 56, in has_table
    return self.Migration._meta.db_table in self.connection.introspection.table_names(self.connection.cursor())
  File "/usr/local/lib/python3.6/dist-packages/django/db/backends/base/base.py", line 256, in cursor
    return self._cursor()
  File "/usr/local/lib/python3.6/dist-packages/django/db/backends/base/base.py", line 233, in _cursor
    self.ensure_connection()
  File "/usr/local/lib/python3.6/dist-packages/django/db/backends/base/base.py", line 217, in ensure_connection
    self.connect()
  File "/usr/local/lib/python3.6/dist-packages/django/db/utils.py", line 89, in __exit__
    raise dj_exc_value.with_traceback(traceback) from exc_value
  File "/usr/local/lib/python3.6/dist-packages/django/db/backends/base/base.py", line 217, in ensure_connection
    self.connect()
  File "/usr/local/lib/python3.6/dist-packages/django/db/backends/base/base.py", line 195, in connect
    self.connection = self.get_new_connection(conn_params)
  File "/usr/local/lib/python3.6/dist-packages/django/db/backends/postgresql/base.py", line 178, in get_new_connection
    connection = Database.connect(**conn_params)
  File "/usr/local/lib/python3.6/dist-packages/psycopg2/__init__.py", line 127, in connect
    conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
django.db.utils.OperationalError: could not connect to server: Connection refused
        Is the server running on host "localhost" (127.0.0.1) and accepting
        TCP/IP connections on port 5433?
could not connect to server: Cannot assign requested address
        Is the server running on host "localhost" (::1) and accepting
        TCP/IP connections on port 5433?
```

right answer - NO (ох и боб)

## 12 / 17
Why did the command not work?

да боб просто долбоеб

right answer - "Connection refused to DB on 127.0.0.1, port 5433"

## 13 / 17

Task 8:
It appears that Bob did not configure his app to connect a postgres database running on a different server.
That explains why things are working on his laptop and not in the DEV servers.
It also appears that he is using the wrong port for postgres!
Find the file in the directory under /opt/caleston-code that has a string matching DATABASES = {.
Replace the value of localhost to devdb01
In the same file fix the postgres port to match the port being used on devdb01

```
bob@devapp01:/opt/caleston-code/mercuryProject$ grep -R "DATABASES = {" .
./mercury/settings.py:DATABASES = {
bob@devapp01:/opt/caleston-code/mercuryProject$ vi mercury/settings.py (ручками поправлю не гордый)
```

## 14 / 17

Task 9:
Now that has been set up, change the ownership of ALL files and directories under /opt/caleston-code to user mercury.
Bob's password is caleston123.

```
bob@devapp01:/opt/caleston-code/mercuryProject$sudo chown -R mercury:mercury /opt/caleston-code/
[sudo] password for bob: 
bob@devapp01:/opt/caleston-code/mercuryProject$ sudo ls -la /opt/caleston-code/
total 40
drwxrwxr-x 6 mercury mercury 4096 Jan  8  2021 .
drwxr-xr-x 1 root    root    4096 Feb 28 10:35 ..
-rw-rw-r-- 1 mercury mercury 1998 Jan  8  2021 .gitignore
drwxrwxr-x 3 mercury mercury 4096 Jan  8  2021 .idea
-rw-rw-r-- 1 mercury mercury    7 Jan  8  2021 README.md
-rw-rw-r-- 1 mercury mercury    0 Jan  8  2021 db.sqlite3
-rw-rw-r-- 1 mercury mercury  634 Jan  8  2021 manage.py
drwxrwxr-x 7 mercury mercury 4096 Jan  8  2021 mercuryProject
drwxrwxr-x 2 mercury mercury 4096 Jan  8  2021 templates
drwxrwxr-x 3 mercury mercury 4096 Jan  8  2021 venv
```

## 15 / 17

Great! Everything should now be in order to restart the application.
On the devapp01 server start the webserver again by running the command:

Navigate to the directory /opt/caleston-code/mercuryProject
Next, run the command
python3 manage.py migrate
and
python3 manage.py runserver 0.0.0.0:8000

Note:- Make sure to activate the virtual environment using source ../venv/bin/activate within the current project before executing python3 manage.py migrate.
Something like (venv) should now be a part of the prompt.
To access the application, click on the Project Mercury tab!

```
bob@devapp01:/opt/caleston-code/mercuryProject$ python3 manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, blog, contenttypes, portfolios, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying blog.0001_initial... OK
  Applying portfolios.0001_initial... OK
  Applying sessions.0001_initial... OK
bob@devapp01:/opt/caleston-code/mercuryProject$ python3 manage.py runserver 0.0.0.0:8000 
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
February 28, 2025 - 10:55:02
Django version 2.2.6, using settings 'mercury.settings'
Starting development server at http://0.0.0.0:8000/
Quit the server with CONTROL-C.
[28/Feb/2025 10:55:29] "GET / HTTP/1.1" 200 2598 (это я зашел посмотреть че эт)
[28/Feb/2025 10:56:05] "GET / HTTP/1.1" 200 2598 (а эт их проверялка GET сделала когда я тыкнул "check")
```

вроде не ругается

## 16 / 17

Well done! Now, for the final task before the client presentation.
Create a new service called mercury.service with the following requirements.
Service name: - mercury.service, WorkingDirectory: - /opt/caleston-code/mercuryProject/, Command to run: /usr/bin/python3 manage.py runserver 0.0.0.0:8000.
Restart on failure and enable for multi-user.target.
Run as user mercury.
Set description: Project Mercury Web Application.
Create the unit file under /etc/systemd/system. Once done, enable and start the mercury.service.

```
[Unit]
Description=Project Mercury Web Application
[Service]
WorkingDirectory=/opt/caleston-code/mercuryProject/
ExecStart=/usr/bin/python3 manage.py runserver 0.0.0.0:8000
User=mercury
Restart=on-failure
RestartSec=10
[Install]
WantedBy=multi-user.target
```
```
bob@devapp01:/opt/caleston-code/mercuryProject$ sudo systemctl daemon-reload
bob@devapp01:/opt/caleston-code/mercuryProject$ sudo systemctl enable --now mercury
bob@devapp01:/opt/caleston-code/mercuryProject$ sudo systemctl status mercury
● mercury.service - Project Mercury Web Application
   Loaded: loaded (/etc/systemd/system/mercury.service; enabled; vendor preset: enabled)
   Active: active (running) since Fri 2025-02-28 11:04:21 UTC; 5s ago
 Main PID: 1942 (python3)
    Tasks: 3 (limit: 77143)
   CGroup: /docker/d3fc35b9465513acc24ed50aaad5cd0075509320ebb8f59857609d2e2c9bf97c/system.slice/mercury.service
           ├─1942 /usr/bin/python3 manage.py runserver 0.0.0.0:8000
           └─1944 /usr/bin/python3 manage.py runserver 0.0.0.0:8000

Feb 28 11:04:21 devapp01 systemd[1]: Started Project Mercury Web Application.
Feb 28 11:04:21 devapp01 python3[1942]: Watching for file changes with StatReloader
Feb 28 11:04:23 devapp01 systemd[1]: mercury.service: Failed to reset devices.list: Operation not permitted
bob@devapp01:/opt/caleston-code/mercuryProject$ netstat -ntlp | grep 8000
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
tcp        0      0 0.0.0.0:8000            0.0.0.0:*               LISTEN      -                   
bob@devapp01:/opt/caleston-code/mercuryProject$ curl devapp01:8000
<!doctype html>
<html lang="en">
<head>
  
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <meta name="description" content="">
  <meta name="author" content="">
```

работает

## 17 / 17

Congratulations! You did it! Just in the nick of time too!
You should now be able to access the web application by clicking on the Project Mercury tab above the terminal.

да это замечательно только боба долбоеба повысят а меня даже на работу не возьмут лол:)

Наверное Боб хорошо умеет работать язычком:)