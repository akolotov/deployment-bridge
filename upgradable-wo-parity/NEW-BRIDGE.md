## How to create group_vars file for a new bridge deployment

If you deployed a new bridge and want it to be preconfigured for the future, you need to create an `.yml` file in `group_vars/` folder of this playbook.

Basically, you can use `sokol-kovan.yml` as a template:
```
### home side rpc
home_rpc_url: https://sokol.poa.network
home_rpc_port: 443

### foreign side rpc
foreign_rpc_url: https://kovan.infura.io/mew
foreign_rpc_port: 443

### bridge configs
bridge_deposit_relay_gas:    3000000
bridge_withdraw_relay_gas:   3000000
bridge_withdraw_confirm_gas: 3000000

bridge_deposit_relay_gas_price:    1000000000
bridge_withdraw_relay_gas_price:   1000000000
bridge_withdraw_confirm_gas_price: 1000000000

bridge_authorities:
  - "0xe388c256c31ff953343ce81160b5ca9b564c1a32"
  - "0xbbefa45868cb8d6d445b78592175e4f1049570b0"
  - "0x2822e60af67f3713e696d80281e7e62fc6619dfe"
bridge_authorities_requires_signatures: 1

bridge_home_required_confirmations: 0
bridge_foreign_required_confirmations: 0

bridge_home_contract_address: "0x98f7b68C0Ef6A7DA0Bb0E786144A87bfEcc5cbD1"
bridge_foreign_contract_address: "0x5c29759020Fa2251B6481A3Ac1Ee507Ddbdc075c"
bridge_home_contract_deploy: 2213129
bridge_foreign_contract_deploy: 7066466
```

Let's examine available options:
* `*_rpc_url`: url of the rpc endpoint of the home-side of the bridge
* `*_rpc_port`: port to use (for https use 443)
* `bridge_*` options are directly related to the values in `config.toml` and `db.toml`, see `roles/bridge/templates/config.toml.j2` and `roles/bridge/templates/db.toml.j2` for more details.
* `bridge_authorities` should be set to an array of authorities addresses, one per line starting with dash `-`, like this:
```
bridge_authorities:
  - "0x1234.."
  - "0xabcd.."
```
