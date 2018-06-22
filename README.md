# Genesis

Welcome to EOS Force!

EOS Force is an EOSIO software based blockchain focusing on the security and stablity.

[Learn more about EOS Force](https://github.com/eosforce/eosforce).

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

- Copy `genesis.json`, `System.abi` and `System.wasm` to `/data/eosforce`:

    ```bash
    $ cp genesis.json *.abi *.wasm /data/eosforce
    ```

- Start a node with docker:

    ```bash
    $ mkdir -p /data/nodeos/eosforce
    $ docker run -d --restart=always --name eosforce -v /data/eosforce:/opt/eosio/bin/data-dir -v /data/nodeos/eosforce:/root/.local/share/eosio/nodeos -p 8888:8888 -p 9876:9876 eosforce/eos:v1.0 nodeosd.sh
    ```

- Docker status:

    - `docker container ls`: check if the container is running.
    - `docker logs -f eosforce`: check the log of container `eosforce`.

## Register as a BP

- First of all, create an account and a pair of EOS keys for your BP, which will be used to fill in the `producer-name` and `signature-provider` items, respectively.

- Ensure you have created or activated an account with enough balance.

- Then register as a BP via [`updatebp`](https://github.com/eosforce/contracts/tree/master/System#updatebp). Check out if you are on the BP list with `get table eosio eosio bps` when you have succeeded to finish the BP registration .

- Lastly, call on your supporters to [`vote`](https://github.com/eosforce/contracts/tree/master/System#vote) for you! With enough votes, you should be able to participate in producing blocks.

Refer to [command reference](https://github.com/eosforce/contracts/tree/master/System#command-reference) for all the related commands for BP registration.

## Contact

- Telegram:
    - https://t.me/EOSForce
    - https://t.me/eosforce_en
    - https://t.me/eosforce01

