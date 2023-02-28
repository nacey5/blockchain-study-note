# 区块链学习笔记

## q1:拜占庭一般问题和容错
拜占庭将军问题是一个经典的分布式计算问题，涉及多个节点之间的通信和决策。该问题源于想象一支由多位将军组成的军队，这些将军分别率领不同的部队，必须协调行动以攻击或撤退。问题在于，这些将军之间必须通过通信来共同决定攻击还是撤退，但是其中一些将军可能是叛徒，会发送虚假的信息，从而导致其他将军做出错误的决定。

拜占庭将军问题的目标是设计一种算法，使得在存在最多f个叛徒的情况下，能够确保其他将军做出正确的决策。这个问题的解决方案涉及到容错性，即能够在存在一定数量的错误或故障的情况下，依然能够保证系统的正确性和可靠性。

在拜占庭将军问题中，使用了一些技术来实现容错性。其中包括：

- 去中心化：系统中不存在单点故障，每个节点都是平等的，任何节点的故障都不会影响整个系统的正确性。

- 冗余计算：系统中有多个节点执行相同的任务，如果一个节点出现故障或者发送了错误的信息，其他节点可以比较它们之间的差异，从而排除错误的节点。

- 消息认证：为了防止叛徒发送虚假的信息，每个节点必须对收到的消息进行认证，以确定它们来自于可信的节点。

- 投票机制：节点之间通过投票来达成共识，如果一个节点收到了大多数节点的同意票，就可以确定这个决策是正确的。

通过这些技术，拜占庭将军问题可以在一定程度上实现容错性，从而确保系统的正确性和可靠性。

## 加密算法
以太坊使用 Keccak256 作为它的散列算法。

## 区块链组件
EVM ( Ethereum Virtual Machine 以太坊虚拟机）、矿工、区块、交易、共识算法、账户、智能合约、挖矿、以太币和gas.

## 以太坊结构
![image](https://user-images.githubusercontent.com/85286598/220414354-94f2bdb9-ce50-48f8-b082-4c81e49ce8e0.png)

## 创世区块
这个区块是在链初次发起时·自动创建的 你也可以这样认为，整个链条是由创世区块（通过 genesis json文件来生成）作为第一个区块而开始启动的。
这个概念很重要，因为手动编写智能合约之后，需要由合约创建创世区块。

## 区块头和它的组成部分
![image](https://user-images.githubusercontent.com/85286598/221400382-d10c914e-a06d-4754-9b73-99094fa1cd67.png)


## 初始化--命令
~~~shell
#路径
export GETHROOT=/opt/git/go-ethereum
export PATH=$PATH:$GETHROOT/build/bin
#初始化
geth init ".\genesis.json" --datadir ".\chaindata"
#开启服务
geth --datadir "/root/geth-code/chaindata" --rpc --rpcaddr "0.0.0.0" --rpcapi "eth,web3,miner,admin,personal,net" --rpccorsdomain "*" --nodiscover --networkid 15
#ipc客户端登录
geth attach geth.ipc

ps -ef | grep -i geth
~~~

## 创世区块
这个区块是在链初次发起时·自动创建的 你也可以这样认为，整个链条是由创世区块（通过 genesis json文件来生成）作为第一个区块而开始启动的。
这个概念很重要，因为手动编写智能合约之后，需要由合约创建创世区块。

~~~ json
{
"config":{
"chainId":15,
"homesteadBlock": 0,
"eip155Block": 0,
"eip158Block":0
},
"nonce":"0x0000000000000042",
"mixhash":"0X0000000000000000000000000000000000000000000000000000000000000000",
"difficulty":"0x200",
"alloc":{},
"coinbase":"0x0000000000000000000000000000000000000000",
"timestamp":"0x00",
"parentHash":"0x000000000000000000000000000000000000000000000000000000000000000",
"gasLimit":"0xffffffff",
"alloc":{
}
}
~~~

## 创建账户
personal.newAccount()

## 安装Solidity编译器
npm install -g solc

## 安装web3
npm install web3@0.19

## 连接以太坊
-在node模式下，输入以下命令可以连接到以太坊
~~~ solidity
var Web=require('web3')
var web=new Web(Web.providers.HttpProvider('http://localhost:8545'))
~~~
