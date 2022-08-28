# Hyperledger Fabric 测试网络（自定义）

## Ⅰ 网络组成

| 组织 | 排序 | 通道 |
| ---- | ---- | ---- |
| 4    | 2    | 2    |

## Ⅱ 相关命令

### 1. 根据配置文件生成相关密钥（命令代替CA）

cryptogen generate --config=crypto-config.yaml

### 2. 生成创世块文件

configtxgen -profile OrdererGenesis -outputBlock ./channel-artifacts/genesis.block -channelID fabric-channel

### 3. 生成通道文件（channel12和channel34）

configtxgen -profile Channel12 -outputCreateChannelTx ./channel-artifacts/channel12.tx -channelID mychannel12
configtxgen -profile Channel34 -outputCreateChannelTx ./channel-artifacts/channel34.tx -channelID mychannel34

### 4. 生成组织锚节点文件

configtxgen -profile Channel12 -outputAnchorPeersUpdate ./channel-artifacts/Org1MSPanchors.tx -channelID mychannel12 -asOrg Org1MSP
configtxgen -profile Channel12 -outputAnchorPeersUpdate ./channel-artifacts/Org2MSPanchors.tx -channelID mychannel12 -asOrg Org2MSP
configtxgen -profile Channel34 -outputAnchorPeersUpdate ./channel-artifacts/Org3MSPanchors.tx -channelID mychannel34 -asOrg Org3MSP
configtxgen -profile Channel34 -outputAnchorPeersUpdate ./channel-artifacts/Org4MSPanchors.tx -channelID mychannel34 -asOrg Org4MSP
