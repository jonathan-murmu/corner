# Pull base image
FROM python:3.6

# Set environment varibles
# Prevents Python from writing pyc files to disc
ENV PYTHONDONTWRITEBYTECODE 1
# Prevents Python from buffering stdout and stderr
ENV PYTHONUNBUFFERED 1

# Set work directory
RUN mkdir /code
WORKDIR /code

RUN apt-get update \
    && apt-get install -y netcat

# Install dependencies
RUN pip install pipenv
COPY Pipfile Pipfile.lock /code/
RUN pipenv install --system

# copy entrypoint.sh
COPY ./entrypoint.sh /code/entrypoint.sh
RUN chmod 755 /code/entrypoint.sh

# Copy project
COPY . /code/

# run entrypoint.sh
ENTRYPOINT ["/code/entrypoint.sh"]

# Server
#EXPOSE 8000
#STOPSIGNAL SIGINT
#ENTRYPOINT ["python", "corner_api/manage.py"]
#CMD ["runserver", "0.0.0.0:8000"]
