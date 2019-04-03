FROM img_leanbase:latest 
MAINTAINER Lean <leandro.rawicz@coinfabrik.com>

WORKDIR  root/ethereum

COPY /files/* ./

RUN add-apt-repository -y ppa:ethereum/ethereum && \
        apt-get install ethereum  -y  && \
        geth version && \
	git clone https://github.com/lrawiczNC/explorer.git  && \
        cd explorer && \
        npm install && \
	cd .. && \
	git clone https://github.com/cubedro/eth-net-intelligence-api && \
	cd eth-net-intelligence-api && \
	npm install && \
	cd .. && \
	mkdir node && \
	geth --datadir="./node"  init Genesis.json && \
        pm2 start node.sh && \
        sleep 4 && \
        echo "personal.newAccount('asd'); miner.start(); admin.sleepBlocks(10); miner.stop()" | \
        geth attach ipc:./node/geth.ipc && \
        rm -rf node/

EXPOSE 8545
EXPOSE 8000
