# kodekloud free labs devops services

Great things never came from comfort zones.

– Tony Luziaya

## 1 / 12
Which of the following is not valid systemctl command?

right answer - "systemctl httpd stop"

## 2 / 12
What is the status of httpd service?

We have pre-installed httpd (apache package) which is used for hosting web server.


NOTE: Don't forget to make use of the sudo command.

```
thor@host01 ~$ sudo systemctl status httpd
○ httpd.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; preset: disabled)
     Active: inactive (dead)
       Docs: man:httpd.service(8)
```

right answer - "inactive (dead)"

## 3 / 12

Lets start httpd service so that our host01 can act as web server.
We have pre-installed httpd (apache package) which is used for hosting web server.
NOTE: Don't forget to make use of the sudo command.

```
thor@host01 ~$ sudo systemctl enable --now httpd
Created symlink /etc/systemd/system/multi-user.target.wants/httpd.service → /usr/lib/systemd/system/httpd.service.
thor@host01 ~$ sudo systemctl status httpd
● httpd.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; preset: disabled)
     Active: active (running) since Thu 2025-02-27 17:23:08 UTC; 2s ago
       Docs: man:httpd.service(8)
   Main PID: 5983 (httpd)
     Status: "Started, listening on: port 80"
      Tasks: 177 (limit: 411434)
     Memory: 14.8M
     CGroup: /docker/a1d2b14236bc2faaed6c820242c5b07f6164ee6644fbae46668aedb0c052c43a/system.slice/httpd.service
             ├─5983 /usr/sbin/httpd -DFOREGROUND
             ├─5990 /usr/sbin/httpd -DFOREGROUND
             ├─5991 /usr/sbin/httpd -DFOREGROUND
             ├─5992 /usr/sbin/httpd -DFOREGROUND
             └─5993 /usr/sbin/httpd -DFOREGROUND

Feb 27 17:23:08 host01.mycorp.org httpd[5983]: Server configured, listening on: port 80
```

## 4 / 12

Now we have to enable httpd service so that it starts automatically when system boots up and we dont need to manually start the service.

i did it early on step 3/12

## 5 / 12
Now we decided to use dedicated python flask app instead of apache so please stop httpd service.

```
thor@host01 ~$ sudo systemctl stop httpd
thor@host01 ~$ ^C
thor@host01 ~$ sudo systemctl status httpd
○ httpd.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; preset: disabled)
     Active: inactive (dead) since Thu 2025-02-27 17:24:44 UTC; 8s ago
   Duration: 1min 34.769s
       Docs: man:httpd.service(8)
    Process: 5983 ExecStart=/usr/sbin/httpd $OPTIONS -DFOREGROUND (code=exited, status=0/SUCCESS)
   Main PID: 5983 (code=exited, status=0/SUCCESS)
     Status: "Total requests: 0; Idle/Busy workers 100/0;Requests/sec: 0; Bytes served/sec:   0 B/sec"

Feb 27 17:23:08 host01.mycorp.org httpd[5983]: Server configured, listening on: port 80
```

## 6 / 12

Now we have to disable httpd service so that it doesn't start automatically when system boots up.

okay boss

```
thor@host01 ~$ sudo systemctl disable httpd
Removed "/etc/systemd/system/multi-user.target.wants/httpd.service".
```

## 7 / 12

We have added a new python flask based service called app. In which systemd unit file is this service configured?

```
thor@host01 ~$ systemctl status app
○ app.service - My python web application
     Loaded: loaded (/usr/lib/systemd/system/app.service; disabled; preset: disabled)
     Active: inactive (dead)
```

right answer - "/usr/lib/systemd/system/app.service"

## 8 / 12

What is the status of app service?

right answer - "inactive (dead)" (see prev. stdout)

## 9 / 12

Look at the service configuration file (systemd unit file) and identify which script is run before the app service starts.

okay bossy:

```
thor@host01 ~$ cat /usr/lib/systemd/system/app.service
[Unit]
Description=My python web application

[Service]
ExecStart=/usr/bin/python3 /opt/code/my_app.py
ExecStartPre=/bin/bash /opt/code/configure_db.sh
ExecStartPost=/bin/bash /opt/code/email_status.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

right answer - "/opt/code/configure_db.sh" (сначала пускай базу потом приложение же)

## 10 / 12

Which script is run after app service starts?

right answer - "/bin/bash /opt/code/email_status.sh"

## 11 / 12

Now lets start app service so that our host01 can act as Flask server as we intended.

```
thor@host01 ~$ sudo systemctl start app
thor@host01 ~$ systemctl status app
● app.service - My python web application
     Loaded: loaded (/usr/lib/systemd/system/app.service; disabled; preset: disabled)
     Active: active (running) since Thu 2025-02-27 17:32:30 UTC; 4s ago
    Process: 8262 ExecStartPre=/bin/bash /opt/code/configure_db.sh (code=exited, status=0/SUCCESS)
    Process: 8264 ExecStartPost=/bin/bash /opt/code/email_status.sh (code=exited, status=0/SUCCESS)
   Main PID: 8263 (python3)
      Tasks: 1 (limit: 411434)
     Memory: 18.4M
     CGroup: /docker/a1d2b14236bc2faaed6c820242c5b07f6164ee6644fbae46668aedb0c052c43a/system.slice/app.service
             └─8263 /usr/bin/python3 /opt/code/my_app.py

Feb 27 17:32:30 host01.mycorp.org bash[8262]: ....
Feb 27 17:32:30 host01.mycorp.org bash[8264]: Send email after python app starts
Feb 27 17:32:30 host01.mycorp.org bash[8264]: ....
Feb 27 17:32:30 host01.mycorp.org python3[8263]:  * Serving Flask app 'my_app'
Feb 27 17:32:30 host01.mycorp.org python3[8263]:  * Debug mode: off
Feb 27 17:32:30 host01.mycorp.org python3[8263]: WARNING: This is a development server. Do not use it in a production deployment.>
Feb 27 17:32:30 host01.mycorp.org python3[8263]:  * Running on all addresses (0.0.0.0)
Feb 27 17:32:30 host01.mycorp.org python3[8263]:  * Running on http://127.0.0.1:8081
Feb 27 17:32:30 host01.mycorp.org python3[8263]:  * Running on http://172.16.238.3:8081
Feb 27 17:32:30 host01.mycorp.org python3[8263]: Press CTRL+C to quit
```

## 12 / 12

Now we have to enable app service so that it starts automatically when system boots up and we dont need to manually start the service.

блин ну сказали бы срау :)

```
thor@host01 ~$ sudo systemctl enable app
Created symlink /etc/systemd/system/multi-user.target.wants/app.service → /usr/lib/systemd/system/app.service.
```


