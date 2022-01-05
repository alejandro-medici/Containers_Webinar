FROM python:3.11.0a3-slim-bullseye

COPY . /usr/src/myapp
WORKDIR /usr/src/myapp

RUN pip install -r requirements.txt

CMD ["python", "main.py"]