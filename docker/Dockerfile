FROM python:latest
ENV PATH=~/.local/bin/:$PATH
RUN pip install awscli --upgrade --user 
RUN apt-get update
RUN apt-get install jq -y