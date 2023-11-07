# Workshop
Adopting Bitcoin '23 repository for the workshop session about NodeGuard

DISCLAIMER: This readme has been run and tested on macOS, it shall be equivalent in Linux

# Requisites
- Docker & Docker Compose
- [Polar Lightning](https://lightningpolar.com/)
# Setup
Follow the steps below to setup the environment for the workshop session.
## 1. Clone the repository
```
git clone https://github.com/Elenpay/workshop-nodeguard
```
## 2. Run the regtest network
1. Open polar lightning
2. Import Network-> Select devnetwork.zip
3. Start the network and enable auto mining
4. Unzip devnetwork.zip to regtest.polar
   ```
   unzip devnetwork.zip -d regtest.polar
   ```
5. Unzip loopd.zip to .loop
    ```
    unzip loopd.zip -d .loop
    ```
6. Bring up the docker-compose in the following order, wait a couple of seconds
```
docker-compose up nbxplorer -d
```
7. Bring everything up except liquidator
```
docker compose up nodeguard loopserver nodeguard_postgres loopserver -d
```
8. Create an api key for liquidator in NG API -> New
9. Paste the api key in the docker.compose.yaml, replace `NODEGUARD_API_KEY` env var of liquidator
10. Start the remaining components
```
docker-compose up -d
```
11.  Add carol and alice nodes, take the info from polar. Make sure to point to `host.docker.internal:grpcport` of each node as endpoints, also the macaroon must be in `hex`
12.  Create a new finance manager user and set the keys.   
13. Create a multisig wallet with the new created key a fund it
14. Open a channel and sign it
15. Set up liquidity rules for the new channel