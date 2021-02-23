## NewChain主网记账节点部署指南

### 1. 购买云服务器，可参考：

https://www.aliyun.com/product/ecs?spm=5176.12825654.eofdhaal5.2.36722c4aSDIOpf

### 2. 按照下面链接代码操作部署主网只读节点，启动区块同步：

https://github.com/newtonproject/newchain-deploy

### 3. 查看区块同步进度：

3.1 执行命令查看同步好的区块高度（number字段对应值）

sudo supervisorctl tail -f newchain stderr

3.2 如同步好的区块链高度与下面链接中的主网最新区块高度一致则同步完成

https://explorer.newtonproject.org

### 4. 同步完成后执行下列命令

```bash
cd /data/newchain/mainnet/ && curl -L https://release.cloud.diynova.com/newton/newchain-deploy/mainnet/newchain-mine.sh -o newchain-mine.sh && chmod +x newchain-mine.sh && ./newchain-mine.sh
```

该命令会下载并运行 newchain-mine.sh 脚本，会创建0x开头的矿工地址，并启用挖矿。

### 5. 设置keystore密码

输入两次keystore密码，保存好keystore和minnner地址

- 备份keystore

输入如下命令，获取keystore内容，

```bash
cat /data/newchain/mainnet/nodedata/keystore/*
```

keystore为整个大括号及其包含的内容，需要备份好，切勿泄露给任何人

- 备份keystore的密码

输入如下命令，即可看到密码

```bash
cat /data/newchain/mainnet/password.txt
```

### 6. 将填写好的如下内容提交至主网稳定运行群，供已存在的主网记账节点审核通过：

* 对外显示名称：
* 第4步中创建好的0x开头矿工地址：
* RPC Url（可以是服务器地址加端口）：
* NewPay社群节点中展示机器节点主体（个人、社群、组织）名称：LEDGER-XXX
* 节点负责人及联系方式（手机、邮箱、微信、telegram等均可）：
* 用于接收主网矿工纪念币的主网NEW地址(NewPay或NewMask)：

或者点击下面链接填写相关信息：

https://github.com/newtonproject/newchain-nodes/issues/new/choose

### 7. Minner地址粘贴替代下列代码中的000:

```bash
/data/newchain/mainnet/bin/geth attach /data/newchain/mainnet/nodedata/geth.ipc --exec 'clique.propose("000", true)'
```

### 8. 批准加入

将替换好自己minner地址的第7项中的命令发送至“NewChain主网记账节点稳定运行群”或者在 “https://github.com/newtonproject/newchain-nodes/issues/new/choose” 填写7中代码请其他矿工执行批准加入。

### 9. 等待其他节点执行代码批准加入

### 10. 查看是否已成为记账节点

```bash
/data/newchain/mainnet/bin/geth attach /data/newchain/mainnet/nodedata/geth.ipc --exec 'clique.getSigners()'
```

