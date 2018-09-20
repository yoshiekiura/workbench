[circleci]: https://circleci.com/gh/rubykube/workbench

# Workbench

[![CircleCI](https://circleci.com/gh/rubykube/workbench.svg?style=svg)][circleci]

Workbench is an easy way to start Peatio development environment.

## Prerequisites

- Docker [installed](https://docs.docker.com/engine/installation/)
- Docker Compose [installed](https://docs.docker.com/compose/install/)

## Usagehttps://github.com/yoshiekiura/workbench.git

### Prepare the workbench

1. Recursive clone

```sh
git clone --recursive https://github.com/yoshiekiura/workbench.git
```

2. Move to workbench

```sh
cd workbench
```

3. Build the images

```sh
make build
```

4. **Optional:** Enable bitcoin

```sh
make bitcoin
```

This will create new seeds and start `bitcoind` docker container.

5. Run the application

```sh
make run
```

You should add those hosts to your `/etc/hosts` file:

```
0.0.0.0 api.zenbitex.com
0.0.0.0 auth.zenbitex.com

0.0.0.0 ws.ranger.zenbitex.com

0.0.0.0 pma.zenbitex.com
0.0.0.0 monitor.zenbitex.com

0.0.0.0 btc.zenbitex.com
0.0.0.0 eth.zenbitex.com

0.0.0.0 mail.zenbitex.com
```

Now you have peatio up and running.

#### Post installation steps

After deployment, height of blockchains should be updated to start receiving deposits.

Go to **Blockchains** Tab in Peatio Admin Panel and update height

Best way to find current blockchains height:

1. [Ethereum Rinkeby Blockchain Explorer](https://rinkeby.etherscan.io)
2. [Bitcoin Testnet Blockchain Explorer](https://testnet.blockchain.info)

#### Barong

Start barong server

```sh
$> docker-compose run --rm barong bash -c "./bin/link_config && ./bin/setup"
$> docker-compose up -d barong
```

This will output password for **admin@barong.io**. Default password is `Qwerty123`

#### Peatio

Start peatio server

```sh
$> docker-compose run --rm peatio bash -c "./bin/link_config && rake db:create db:migrate db:seed"
$> docker-compose up -d peatio
```

#### Frontend

Simply start your local server. Now you're able to log in with your local Barong and Peatio.

## Running Tests

Run toolbox stress tests

```sh
$> make stress
```
