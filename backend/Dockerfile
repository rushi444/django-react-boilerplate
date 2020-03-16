# Use an official Python runtime as a parent image
FROM python:3.7-alpine
LABEL maintainer="rushi444"

# Adding backend directory to make absolute filepaths consistent across services
WORKDIR /app/backend

# Install Python dependencies
COPY requirements.txt /app/backend
RUN apk add --update --no-cache postgresql-client
RUN apk add --update --no-cache --virtual .tmp-build-deps \
    gcc libc-dev linux-headers postgresql-dev
RUN pip3 install --upgrade pip -r requirements.txt
RUN apk del .tmp-build-deps

# Add the rest of the code
COPY . /app/backend

# Make port 8000 available for the app
EXPOSE 8000

# Be sure to use 0.0.0.0 for the host within the Docker container,
# otherwise the browser won't be able to find it
CMD python3 manage.py runserver 0.0.0.0:8000
