### Install

```shell
# install vyper
virtualenv -p python3 venv
source venv/bin/activate
pip install vyper

cp .env.sample .env
```

### For windows

```
virtualenv -p python3 venv
venv\Scripts\activate
pip install vyper

```

### To run

```
venv\Scripts\activate
truffle compile

```

### Test

```shell
source .env

# using infura.io
npx ganache-cli \
--fork https://mainnet.infura.io/v3/$WEB3_INFURA_PROJECT_ID \
--unlock $WETH_WHALE \
--unlock $DAI_WHALE \
--unlock $USDC_WHALE \
--unlock $USDT_WHALE \
--unlock $WBTC_WHALE \
--networkId 999

# using archivenode.io (limit 10 req / sec)
## fork at block
BLOCK=11597142
ARCHIVE_NODE_URL=https://api.archivenode.io/$ARCHIVE_NODE_API_KEY@$BLOCK
## latest block
ARCHIVE_NODE_URL=https://api.archivenode.io/$ARCHIVE_NODE_API_KEY

ganache-cli \
--fork $ARCHIVE_NODE_URL \
--unlock $WETH_WHALE \
--unlock $DAI_WHALE \
--unlock $USDC_WHALE \
--unlock $USDT_WHALE \
--unlock $WBTC_WHALE \
--networkId 999

# run test
env $(cat .env) npx truffle test --network mainnet_fork test/test-erc20.js
env $(cat .env) npx truffle test --network mainnet_fork test/test-dydx-solo-margin.js
```

1. 使用的是mainnet.infura.io，不是alchemyapi.io，infuro的主网在https://infura.io/，需要自己去注册project获取WEB3_INFURA_PROJECT_ID
2. 我不用vyper，truffile compile前把contracts下面的vy文件迁移走
3. BLOCK=11597142是用原来readme里的
4. truffle compile的时候solc版本可能不对，需要改一下truffle.config.js里的version为^0.8.0
