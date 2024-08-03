FROM python:3.13.0rc1-slim-bullseye

COPY . /usr/src/myapp
WORKDIR /usr/src/myapp

RUN pip install -r requirements.txt

CMD ["python", "main.py"]