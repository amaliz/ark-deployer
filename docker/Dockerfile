FROM node:latest

RUN apt-get update && apt-get install -y curl build-essential python git

RUN apt-get install -y postgresql postgresql-contrib

#RUN adduser --disabled-password --gecos '' ark
RUN groupadd --gid 1001 ark && useradd --uid 1001 --gid ark --shell /bin/bash --create-home ark

RUN  npm install -g n && n 6.9.2 && npm install grunt-cli -g

USER ark

WORKDIR /home/ark

RUN mkdir arknode && \
    git clone https://github.com/arkecosystem/ark-node.git arknode && \
   cd arknode && \
   npm install libpq secp256k1 && \
   npm install
WORKDIR /home/ark/arknode

# USER postgres

# RUN /etc/init.d/postgresql start && createuser --superuser ark

# RUN createdb ark_testnet

COPY ./config.json config.json

USER root

RUN apt-get install -y vim

USER ark

EXPOSE 4000

CMD ["node","app.js","--genesis","genesisBlock.testnet.json","--config","config.json"]

#USER postgres

#RUN createuser --createdb --password ark && createdb ark_test

#USER root

#RUN npm install -g n && n 6.9.2 && npm install grunt-cli -g

#
