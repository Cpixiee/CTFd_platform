**Installing Server CTFd on Debian Server**

$ apt update -y && sudo apt upgrade -y

$ adduser ctfd

$ su - ctfd

$ apt install -y python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools nginx git

$ mkdir /var/log/CTFd

$ chown ctfd. /var/log/CTFd

$ git clone https://github.com/CTFd/CTFd.git

$ cd CTFd

$ pip3 install -r requirements.txt

$ pip3 install gunicorn

$ nano /etc/systemd/system/ctfd.service
[This File](https://github.com/Cpixiee/CTFd_platform/blob/main/this_file.md)

$ sudo systemctl daemon-reload

$ sudo systemctl enable ctfd.service

$ sudo systemctl start ctfd.service


$ gunicorn --bind 0.0.0.0:8000 -w 4 "CTFd:create_app()"
