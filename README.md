# There are steps to run validator client on helder testnet by using docker

## Run EL
### Init the setup first.
```
docker compose run --rm geth init --datadir=/data/geth/execution-data --state.scheme=hash /network-configs/genesis.json
```
### Run node
```
docker compose up -d geth
```

## Run CL
```
docker compose up -d lighthouse
```

## Run VC
### Generate validator keystores first.
### Run node
```
docker compose up -d validator
```
It's failed atm
### Update `/helder-nodes/validator/validator-data/validators/validator_definitions.yml` to add `voting_keystore_password_path` field
For example:
```
- enabled: true
  voting_public_key: 0x8aa5bbee21e98c7b9e7a4c8ea45aa99f89e22992fa4fc2d73869d77da4cc8a05b25b61931ff521986677dd7f7159e8e6
  description: 0x8aa5bbee21e98c7b9e7a4c8ea45aa99f89e22992fa4fc2d73869d77da4cc8a05b25b61931ff521986677dd7f7159e8e6
  type: local_keystore
  voting_keystore_path: /data/lighthouse/validator-data/validators/keytores/keys/0x8aa5bbee21e98c7b9e7a4c8ea45aa99f89e22992fa4fc2d73869d77da4cc8a05b25b61931ff521986677dd7f7159e8e6/voting-keystore.json
  voting_keystore_password_path: /data/lighthouse/validator-data/validators/keytores/secrets/0x8aa5bbee21e98c7b9e7a4c8ea45aa99f89e22992fa4fc2d73869d77da4cc8a05b25b61931ff521986677dd7f7159e8e6 # Added this line

```
### Re-run node
```
docker compose up -d validator
```