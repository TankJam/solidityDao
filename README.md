# solidityDao
2022 年是DAO 元年。同时为了更深一步理解DAO原理，自己动手从零到一做一个。也许这是你朋友的模因 DAO。也许这是一个旨在解决气候变化的 DAO。由你决定。
我们将讨论诸如创建会员 NFT、创建/空投代币、公共国债和使用代币进行治理之类的事情！


## 一 Dao介绍
### 1、什么是Dao？
- 去中心化自治组织 (DAO) 是一个没有中央领导的实体。比如有个银行账号属于这个Dao组织，那么这个账号的所有操作都需要通过提案，由组织下的人进行投票，
最高的选票即为最终决策，最后提案就会在链上执行;
- DAO 只是一群拥有共享银行账户的陌生人，他们就如何使用该银行账户进行投票。 如果您仍然没有得到它，请不要担心。让我们通过代码来自己构建一个:)。

### 2、案例
- AnimeDAO — 一个动漫爱好者社区，只要他们与社区互动并谈论动漫，就会收到 $ANIME。
- PizzaDAO — 一个专注于赠送披萨的慈善 DAO。会员可以向慈善机构捐赠 ETH，并获得 $PIZZA 作为回报。
- FarzaDAO — Farza粉丝的 DAO，只要他们在推特上发布有关 Farza 的好消息，就会收到 $FARZA。
- ArtistDAO — 一个由艺术家组成的 DAO，为各级艺术家举办活动和研讨会。每当会员举办活动或研讨会时，他们都会收到 $ARTIST。
- 巴基斯坦DAO——巴基斯坦创业社区成员互相支持的DAO。只要成员向其他创始人提供价值，例如通过向他们提供建议、对他们的产品进行 Beta 测试或在社交媒体上支持他们，他们就会赚取 $PAKISTAN。

### 3、工作原理
- 通过募捐的形式，一群用户共享一个银行账户，通过投票作出投资等各种行为;

## 二 为DAO设置客户端应用程序
### 1、项目构建流程
- 1）构建一个网络应用程序
- 2）连接用户的钱包 
- 3）铸造会员 NFT 
- 4）接收代币空投 
- 5）并对提案进行实际投票。

Web 应用程序其实就是“DAO 仪表板”。这是所有新用户可以加入的地方，它允许DAO成员查看 DAO 在做什么。

### 2、通过react实现连接钱包

## 三 创建会员NFT
### 1、ThirdWeb（https://github.com/thirdweb-dev/contracts）
- ThirdWeb可以提供一套工具，无需编写任何Solidity即可创建智能合约，但是需要通过javascript编写脚本来创建与部署智能合约。
- 1）通过 https://thirdweb.com/contracts 进入面板，连接钱包，并创建项目名称
- 2）支付费用后，则是在链上部署的合约创建容器，thirdweb没有数据库，所有数据都存储在链上;

### 2、配置.env（钱包地址、钱包秘钥、AlchemyApi）

### 3、初始化SDK
- scripts/1-initialize-sdk.js
```javascript
import { ThirdwebSDK } from "@3rdweb/sdk";
import ethers from "ethers";
//导入和配置我们用来安全存储环境变量的 .env 文件。
import dotenv from "dotenv";
dotenv.config();
// 一些快速检查以确保我们的 .env 工作正常。
if (!process.env.PRIVATE_KEY || process.env.PRIVATE_KEY == "") {
  console.log("🛑 Private key not found.")
}
if (!process.env.ALCHEMY_API_URL || process.env.ALCHEMY_API_URL == "") {
  console.log("🛑 Alchemy API URL not found.")
}
if (!process.env.WALLET_ADDRESS || process.env.WALLET_ADDRESS == "") {
  console.log("🛑 Wallet Address not found.")
}
const sdk = new ThirdwebSDK(
  new ethers.Wallet(
    // 您的钱包私钥。始终保持私密，不要与任何人分享，将其添加到您的 .env 文件中并不要将该文件提交到 github！
    process.env.PRIVATE_KEY,
    // RPC URL, we'll use our Alchemy API URL from our .env file.
    ethers.getDefaultProvider(process.env.ALCHEMY_API_URL),
  ),
);
(async () => {
  try {
    const apps = await sdk.getApps();
    console.log("Your app address is:", apps[0].address);
  } catch (err) {
    console.error("Failed to get apps from the sdk", err);
    process.exit(1);
  }
})()
// 我们正在导出初始化的thirdweb SDK，以便我们可以在其他脚本中使用它
export default sdk;
```


### 4、创建一个ERC-1155集合
### 5、部署NFT元数据
### 6、设置mint条件（一）
### 7、设置mint条件（二）
### 8、检查用户是否拥有NFT
### 9、用户mint NFT 会员卡
### 10、用户拥有NFT时才显示 DAO Dashboard


## 四 Token + 链上治理
### 1、部署ERC-20合约
### 2、MetaMask钱包 “导入令牌”
### 3、创建代币供应
### 4、空投治理Token
### 5、在 Dao Dashboard 上展示Token持有者
### 6、在 Dao Dashboard 上呈现成员数据
### 7、部署治理合约
### 8、设置金库
### 9、创建前两个DAO提案
### 10、让用户对仪表板中的提案进行投票

## 五 收尾工作
### 1、撤销角色
### 2、处理基本的不受支持的网络错误
### 3、自定义网络应用程序
### 4、完成并庆祝😁

  