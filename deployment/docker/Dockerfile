FROM python:3.9.5
ADD ./  /app
RUN pip install flask
RUN pip install pyopenssl
RUN openssl req -new -newkey rsa:4096 -days 3650 -nodes -x509 -subj '/C=TH/ST=TH/L=BKK/O=CTS/CN=mycert' -keyout key.pem -out cert.pem
WORKDIR /app
CMD [ "python", "./upload.py" ]
