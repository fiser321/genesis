# Genesis

EOS Force Genesis is comprised of these elements:

- [accounts_eosforce.csv](csv/accounts_eosforce.csv)
- [accounts_famous.csv](csv/accounts_famous.csv)
- [accounts_snapshot.csv](csv/accounts_snapshot.csv)
- [keys_biosbp.csv](csv/keys_biosbp.csv)

[Learn more about EOS Force](https://github.com/eosforce/eosforce).

This repo also maintains the document of running EOS Force node via docker.

## Run a node via Docker

- Clone this project:

    ```bash
    $ git clone https://github.com/eosforce/genesis.git
    $ cd genesis
    ```

- Modify the lines with `NOTE:` mark in `config.ini` accordingly, then copy the revised `config.ini` to `/data/eosforce`:

    ```bash
    $ mkdir -p /data/eosforce
    # Copy the modified config.ini to /data/eosforce
    $ cp config.ini /data/eosforce
    ```

- Copy `genesis.json`, `System.abi`, `System.wasm`, `eosio.token.abi` and `eosio.token.wasm` to `/data/eosforce`:

    ```bash
    $ cp genesis.json *.abi *.wasm /data/eosforce
    ```

- Start a node with docker:

    ```bash
    $ mkdir -p /data/nodeos/eosforce
    $ docker run -d --restart=always --name eosforce -v /data/eosforce:/opt/eosio/bin/data-dir -v /data/nodeos/eosforce:/root/.local/share/eosio/nodeos -p 8888:8888 -p 9876:9876 eosforce/eos:v1.0 nodeosd.sh
    ```

- Docker status:

    ```bash
    # enter docker
    $ docker exec -it eosforce bash

    $ cleos wallet create

    $ cleos import <your-private-key>
    ```

    - `docker container ls`: check if the container is running.
    - `docker logs -f eosforce`: check the log of container `eosforce`.

    Refer to [eosforce/contracts/System](https://github.com/eosforce/contracts/tree/master/System#command-reference) for more details about `transfer`, `vote` etc.

## Register as a BP

- First of all, create an account and a pair of EOS keys for your BP, which will be used to fill in the `producer-name` and `signature-provider` items, respectively.

- Ensure you have created or activated an account with enough balance.

- Then register as a BP via [`updatebp`](https://github.com/eosforce/contracts/tree/master/System#updatebp). Check out if you are on the BP list with `get table eosio eosio bps` when you have succeeded to finish the BP registration .

    ```bash
    # bpname will be used as producer-name in config.ini.
    # block_signning_key pair will be used as signature-provider in config.ini.
    # commission_rate's range is [0, 10000], which means [0%, 100%]. If the commission_rate is 1000, e.g., 10%, then you'll take 10% of your block rewards and give 90% to your voters.
    $ cleos push action eosio updatebp '{"bpname":"your_bp_name", "block_signing_key":"EOSXXX", "commission_rate":"1000", "url":"http://eosforce.io"}' -p your_bp_name
    ```

- Lastly, call on your supporters to [`vote`](https://github.com/eosforce/contracts/tree/master/System#vote) for you! With enough votes, you should be able to participate in producing blocks.

    ```bash
    # stake: quantity, e.g., `100.0000 EOS`
    $ cleos push action eosio vote '{"voter":"voter", "bpname":"bpname", "stake":"stake"}' -p voter
    ```

Refer to [command reference](https://github.com/eosforce/contracts/tree/master/System#command-reference) for all the related commands for BP registration.

## Contact

- Telegram:
    - https://t.me/EOSForce
    - https://t.me/eosforce_en
    - https://t.me/eosforce01

