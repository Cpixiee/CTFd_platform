[Unit]
Description=CTFd Service
After=network.target

[Service]
User=ctfd
Group=ctfd
WorkingDirectory=/path/to/your/ctfd
ExecStart=/usr/bin/python3 /path/to/your/ctfd/serve.py
Restart=always
Environment="FLASK_ENV=production"
Environment="PORT=8000"

[Install]
WantedBy=multi-user.target
