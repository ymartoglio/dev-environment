FROM    ubuntu:16.04

# update package repo first
RUN apt-get update

# node 6 install
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -

# install needed packages nodejs, npm, git, ...d
RUN apt-get install -y nodejs git git-core ccze

# global packages installation
RUN npm install -g bower
RUN npm install -g nodemon
RUN npm install -g mocha
RUN npm install -g should


# allow port to be accessed from outside
EXPOSE 8080
EXPOSE 5858

# install & launch the app
# bower init --allow-root;
ENTRYPOINT cd /app;npm install --development;nodemon --debug=5858 /app/cm-app/src/server.js | ccze -A
