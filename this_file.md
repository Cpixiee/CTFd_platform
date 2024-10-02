```[Unit]
Description = CTFd
After = network.target

[Service]
PermissionsStartOnly = true
PIDFile = /run/CTFd.pid
User = ctfd
Group = ctfd
WorkingDirectory = /home/ctfd/CTFd
ExecStartPre = /bin/mkdir -p /run/CTFd
ExecStartPre = /bin/chown -R ctfd. /run/CTFd
ExecStart = gunicorn3 --bind 0.0.0.0:8000 -w 4 "CTFd:create_app()"
ExecReload = /bin/kill -s HUP $MAINPID
ExecStop = /bin/kill -s TERM $MAINPID
PrivateTmp = true

[Install]
WantedBy = multi-user.target```
