**Installing Server CTFd on Debian Server**

$ apt update -y && sudo apt upgrade -y

$ adduser ctfd

$ su - ctfd

$ apt install -y python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools nginx git
pip3 install pipenv

$ mkdir /var/log/CTFd

$ chown ctfd. /var/log/CTFd

$ git clone https://github.com/CTFd/CTFd.git

$ cd CTFd

$ pip3 install -r requirements.txt

$ pip3 install gunicorn

$ nano /etc/systemd/system/ctfd.service

[Unit]
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
WantedBy = multi-user.target

$ sudo systemctl daemon-reload
$ sudo systemctl enable ctfd.service
$ sudo systemctl start ctfd.service

$ gunicorn3 --bind 0.0.0.0:8000 -w 4 "CTFd:create_app()"
