FROM python:3.8-slim
ENV PYTHONUNBUFFERED=1
MAINTAINER naresh.p123@gmail.com

WORKDIR /code

COPY requirements.txt /code/
RUN pip install -r requirements.txt
COPY . /code/

# what happens when I start the container
CMD python manage.py runserver 0.0.0.0:8000
