#https://docs.streamlit.io/knowledge-base/tutorials/deploy/docker

# app/Dockerfile

#set the Base Image (think OS) for the container
FROM python:3.8-slim


##The WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile . Let’s set it to app/ :
WORKDIR /app

##Install git so that we can clone the app code from a remote repo:
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    software-properties-common \
    git \
    && rm -rf /var/lib/apt/lists/*

#Clone your code that lives in a remote repo to WORKDIR:
#RUN git clone https://github.com/streamlit/streamlit-example.git .

# Once cloned, the directory of WORKDIR will look like the following:

# app/
# - requirements.txt
# - streamlit_app.py


#Install your app’s Python dependencies from the cloned requirements.txt in the container:
RUN pip3 install -r requirements.txt

#The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime. Your container needs to listen to Streamlit’s (default) port 8501:
EXPOSE 8501

#The HEALTHCHECK instruction tells Docker how to test a container to check that it is still working. Your container needs to listen to Streamlit’s (default) port 8501:
HEALTHCHECK CMD curl --fail http://localhost:8501/_stcore/health

#An ENTRYPOINT allows you to configure a container that will run as an executable. Here, it also contains the entire streamlit run command for your app, so you don’t have to call it from the command line:
ENTRYPOINT ["streamlit", "run", "streamlit_app.py", "--server.port=8501", "--server.address=0.0.0.0"]


### go to ~/.docker/config.json, change credsStore to credStore.
## The docker build command builds an image from a Dockerfile . Run the following command from the app/ directory on your server to build the image:

#docker build -t streamlit .
#The -t flag is used to tag the image. Here, we have tagged the image streamlit

# docker images

# run container
#docker run -p 8501:8501 streamlit
#The -p flag publishes the container’s port 8501 to your server’s 8501 port.


