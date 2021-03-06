# Money On Chain

Python API to Money On Chain projects.

### Requirements

* Python 3.6+ support

### Installation

```
pip3 install moneyonchain
```

### Usage

#### Connection manager 

Connect by default to RSK Testnet public node 

```
from moneyonchain.manager import ConnectionManager

connection_manager = ConnectionManager()
print("Connected: {conectado}".format(conectado=connection_manager.is_connected))
print("Gas price: {gas_price}".format(gas_price=connection_manager.gas_price))
```

#### Connections table

| Network Name      | Project | Enviroment                       | Network    |
|-------------------|---------|----------------------------------|------------|
| mocTestnetAlpha   | MOC     |                                  | Testnet    |
| mocTestnet        | MOC     | moc-testnet.moneyonchain.com     | Testnet    |
| mocMainnet2       | MOC     | alpha.moneyonchain.com           | Mainnet    |
| rdocTestnetAlpha  | RIF     |                                  | Testnet    |
| rdocTestnet       | RIF     | rif-testnet.moneyonchain.com     | Testnet    |
| rdocMainnet       | RIF     | rif.moneyonchain.com             | Mainnet    |
| dexTestnet        | TEX     | xxx.moneyonchain.com             | Testnet    |


#### Token Prices

Get token prices in US Dollars

```
from moneyonchain.manager import ConnectionManager
from moneyonchain.moc import MoC

# Connect to MoC Mainnet enviroment network
network = 'mocMainnet2'
connection_manager = ConnectionManager(network=network)
print("Connecting to %s..." % network)
print("Connected: {conectado}".format(conectado=connection_manager.is_connected))

contract = MoC(connection_manager)
print()
print("Bitcoin price in USD : {:.2f}".format(contract.bitcoin_price()))
print("BPRO price in USD    : {:.2f}".format(contract.bpro_price()))
print("Delta BPRO/BTC       : {:.2%}".format(-1+contract.bpro_price()/contract.bitcoin_price()))
print("BTC2X price in USD   : {:.2f}".format(contract.btc2x_tec_price() * contract.bitcoin_price()))
```

result:

```
Connecting to mocMainnet2...
Connected: True

Bitcoin price in USD : 26466.56
BPRO price in USD    : 31953.54
Delta BPRO/BTC       : 20.73%
BTC2X price in USD   : 30005.24
```

#### Price provider

Get the last price from MOC or RDOC contract.

See example in source/example/price_provider.py

```
from moneyonchain.manager import ConnectionManager
from moneyonchain.price_provider import PriceProvider

import logging
import logging.config

# logging module
# Initialize you log configuration using the base class
logging.basicConfig(level=logging.INFO)
# Retrieve the logger instance
log = logging.getLogger()

# Connect to MoC enviroment network
network = 'mocTestnet'
connection_manager = ConnectionManager(network=network)
log.info("Connecting to %s..." % network)
log.info("Connected: {conectado}".format(conectado=connection_manager.is_connected))

price_provider = PriceProvider(connection_manager)

log.info("Last price: {0}".format(price_provider.price()))

```

result:

```
INFO:root:Connecting to mocTestnet...
INFO:root:Connected: True
INFO:root:Last price: 10725.4
```

RDOC Contract:

```
from moneyonchain.manager import ConnectionManager
from moneyonchain.price_provider import PriceProvider

import logging
import logging.config

# logging module
# Initialize you log configuration using the base class
logging.basicConfig(level=logging.INFO)
# Retrieve the logger instance
log = logging.getLogger()

# Connect to MoC enviroment network
network = 'rdocTestnet'
connection_manager = ConnectionManager(network=network)
log.info("Connecting to %s..." % network)
log.info("Connected: {conectado}".format(conectado=connection_manager.is_connected))

price_provider = PriceProvider(connection_manager)

log.info("Last price: {0}".format(price_provider.price()))
```

Result:

```
INFO:root:Connecting to rdocTestnet...
INFO:root:Connected: True
INFO:root:Last price: 0.092123288999999996
```

#### DOC Token example

Connect to moc-testnet avalaible trought https://moc-testnet.moneyonchain.com
DoCToken is Dollar on Chain Token

``` 
from moneyonchain.manager import ConnectionManager
from moneyonchain.token import DoCToken


network = 'mocTestnet'
connection_manager = ConnectionManager(network=network)
print("Connecting to %s..." % network)
print("Connected: {conectado}".format(conectado=connection_manager.is_connected))

account = '0xCD8a1C9aCC980Ae031456573e34Dc05CD7dAE6e3'

print("Connecting to DoCToken")
doc_token = DoCToken(connection_manager)
print("Token Name: {0}".format(doc_token.name()))
print("Token Symbol: {0}".format(doc_token.symbol()))
print("Total Supply: {0}".format(doc_token.total_supply()))
print("Account: {0} Balance DOC: {1}".format(account, doc_token.balance_of(account)))
```

this print

```
Connecting to mocTestnet...
Connected: True
Connecting to DoCToken
Token Name: Dollar on Chain
Token Symbol: DOC
Total Supply: 62398.334981863939176967
Account: 0xCD8a1C9aCC980Ae031456573e34Dc05CD7dAE6e3 Balance DOC: 443.294681738027382034
```


#### RIF Token example balance

**Mainnet**

Connect to RDOC Mainnet avalaible trought https://rif.moneyonchain.com

``` 
from moneyonchain.manager import ConnectionManager
from moneyonchain.token import RIF


network = 'rdocMainnet'
connection_manager = ConnectionManager(network=network)
print("Connecting to %s..." % network)
print("Connected: {conectado}".format(conectado=connection_manager.is_connected))

account = '0xCD8a1C9aCC980Ae031456573e34Dc05CD7dAE6e3'

print("Connecting to RIF TOKEN")
rif_token = RIF(connection_manager)
print("Token Name: {0}".format(rif_token.name()))
print("Token Symbol: {0}".format(rif_token.symbol()))
print("Total Supply: {0}".format(rif_token.total_supply()))
print("Account: {0} Balance RIF: {1}".format(account, rif_token.balance_of(account)))
```

this print

```
Connecting to rdocMainnet...
Connected: True
Connecting to RIF TOKEN
Token Name: tRIF Token
Token Symbol: tRIF
Total Supply: 1000000000
Account: 0xCD8a1C9aCC980Ae031456573e34Dc05CD7dAE6e3 Balance RIF: 391.072191029720048275
```



**Testnet**

Connect to RDOC Testnet avalaible trought https://rif-testnet.moneyonchain.com

``` 
from moneyonchain.manager import ConnectionManager
from moneyonchain.token import RIF


network = 'rdocTestnet'
connection_manager = ConnectionManager(network=network)
print("Connecting to %s..." % network)
print("Connected: {conectado}".format(conectado=connection_manager.is_connected))

account = '0xCD8a1C9aCC980Ae031456573e34Dc05CD7dAE6e3'

print("Connecting to RIF TOKEN")
rif_token = RIF(connection_manager)
print("Token Name: {0}".format(rif_token.name()))
print("Token Symbol: {0}".format(rif_token.symbol()))
print("Total Supply: {0}".format(rif_token.total_supply()))
print("Account: {0} Balance RIF: {1}".format(account, rif_token.balance_of(account)))
```

this print

```
Connecting to rdocTestnet...
Connected: True
Connecting to RIF TOKEN
Token Name: tRIF Token
Token Symbol: tRIF
Total Supply: 1000000000
Account: 0xCD8a1C9aCC980Ae031456573e34Dc05CD7dAE6e3 Balance RIF: 391.072191029720048275
```



#### Mint BPro example

To run this script need private key, where replace with your PK in **PRIVATE_KEY**, and also you need to have funds in this account

```
martin@martin-desktop:~$ export ACCOUNT_PK_SECRET=PRIVATE_KEY
martin@martin-desktop:~$ python ./example_moc_mint_bpro.py
```

Example code

```
from decimal import Decimal
from web3 import Web3
from moneyonchain.manager import ConnectionManager
from moneyonchain.moc import MoC


network = 'mocTestnet'
connection_manager = ConnectionManager(network=network)
print("Connecting to %s..." % network)
print("Connected: {conectado}".format(conectado=connection_manager.is_connected))

print("Connecting to MoC Main Contract")
moc_main = MoC(connection_manager)

amount_want_to_mint = Decimal(0.001)

total_amount, commission_value = moc_main.amount_mint_bpro(amount_want_to_mint)
print("To mint {0} bitpro need {1} RBTC. Commision {2}".format(format(amount_want_to_mint, '.18f'),
                                                               format(total_amount, '.18f'),
                                                               format(commission_value, '.18f')))

# Mint BPro
# This transaction is not async, you have to wait to the transaction is mined
print("Please wait to the transaction be mined!...")
tx_hash, tx_receipt, tx_logs = moc_main.mint_bpro(amount_want_to_mint)
if tx_logs:
    print("Transaction done!")
    amount = Decimal(Web3.fromWei(tx_logs[0]['args']['amount'], 'ether'))
    amount_usd = moc_main.bpro_amount_in_usd(amount)
    print("You mint {0} BPro equivalent to {1} USD".format(format(amount, '.18f'), format(amount_usd, '.3f')))
else:
    print("Transaction Failed")
```

this print

```
Connecting to mocTestnet...
Connected: True
Connecting to MoC Main Contract
To mint 0.001000000000000000 bitpro need 0.001001000000000000 RBTC. Commision 0.000001000000000000
Please wait to the transaction be mined!...
Transaction done!
You mint 0.000965723337947316 BPro equivalent to 7.107 USD
```
