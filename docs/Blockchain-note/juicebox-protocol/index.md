# Juicebox protocol

## 是什么？

可编程的开支

提前设定把您资金的一部分自动分拨给您想要支持的人或项目，或者您需要支付的贡献者。您获得收入的同时，他们也会收到相应款项。

ERC20 社区代币
当有人向你的项目付款时，他们会收到项目的代币作为回报。 代币可以兑换你项目的部分溢出资金；让你的社区和你共赢。 利用你的项目代币来授予治理权、社区访问权或其他成员福利。

可分派的盈余
设定一个筹款目标以保证计划内的开销。对于超出部分的资金(溢出)，您及其他持有项目代币的人都有权去领取。

透明度&问责制
对项目资金的变动需要经过社区的批准阶段才能生效，这可以作为预防项目方跑路的措施。项目支持者不需要依赖于对你的信任 —— 尽管他们已经这样做了。

## 背景介绍

Juicebox 给出了 DAO 金库管理的新解法，预先承诺项目所需资金及用途，再向社区筹集资金，从目前运营情况看，它已经吸引了数以百计的筹款项目，并出现了收到整个加密社区关注的 ConstitutionDAO 和 AssangeDAO，Juicebox 的治理实验进展迅猛且已初露锋芒。

## 主要概念介绍

### 溢出

每个项目都可以设定一个资金目标，以ETH或USD为单位。该金额可以是一次性目标，也可以是每个融资周期的重复目标。超过筹款目标的资金被称为溢出，一旦一个资助周期结束，任何溢出都可以用来满足下一个周期的资助目标。

当贡献者支付项目时，他们会收到代币。可以赎回代币以索取一定比例的溢出量。例如，拥有总代币供应量1%的钱包可以赎回这些代币以获取1%的溢出。

### 代币

- 默认情况下，进入 Juicebox 项目的所有付款都会生成代币。这些代币分发给支付的贡献者，以及项目保留代币列表中指定的任何地址。铸造的代币数量取决于支付的金额和weight项目当前的融资周期。项目可以覆盖或扩展此默认行为。
- 默认情况下，该协议使用内部记帐机制将令牌分配给接收者。
- 项目可以直接从协议中发行自己的ERC-20代币以用作其代币。项目也可以自带token，只要符合接口即可。这使得使用 ERC-1155或自定义令牌成为可能。IJBToken
- 一旦项目发行了代币，任何人都可以认领代币，这会将它们从协议的内部记账机制中导出到持有者的钱包中，以便在Web3中使用。项目所有者还可以强制将项目的所有代币直接发行到导出的版本中。这绕过了内部会计机制，但略微增加了每笔需要铸造代币的交易的 gas。
- 默认情况下，持有者可以赎回（销毁）代币，以索取项目溢出中的一部分。
- 项目所有者可以按需铸造和分发更多项目的代币。可以在每个资金周期的基础上暂停此行为。
- 项目可以随心所欲地使用其代币。

### 折扣率

创建项目时，可选择配置一个折扣率用于激励早期支持者。每个新的筹款周期，支付给项目的同等金额所奖励的代币数量将按折扣率递减。

例如：该项目设置了10%的折扣率和14天的期限。我向项目支付5个ETH，并在第一天收到5,000,000个代币。14天后，你支付5ETH，将只收到4,500,000代币。

### 联合曲线比率

联合曲线奖励代币的长期持有者。

不设定筹款目标的话，联合曲线比率选项将会禁用。这一比率决定了在任何特定时间内每赎回一个代币可以获得的溢出金额。在联合曲线比率较低的情况下，每赎回一个代币都会相应地提升所有剩余代币的赎回价值，这样就会形成一个代币长期持有的激励机制。当联合曲线比率为 100% 时，则意味着无论什么时候赎回代币，每个代币获得的价值都将是相同的。

绑定曲线率改变了每个代币可以赎回的溢出量。60% 的绑定曲线率意味着代币可以赎回其对应价值的 60%。其余40%留在国库中，增加其他代币的价值并奖励长期代币持有者。

这个比率决定了每个代币在任何给定时间可以赎回的溢出量。在较低的联合曲线上，赎回代币会增加每个剩余代币的价值，从而产生比其他代币更长时间持有代币的动机。 100% 的默认联合曲线意味着所有代币无论何时被赎回，都将具有相同的价值。在这个简短的视频中了解更多信息。

> ![联合曲线比率](https://1815966075-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FoYtfVbWpOw09hrlY6W9u%2Fuploads%2Fgit-blob-fd93ec959da54f6178f0ad8b0fa937264b989465%2FCapture2.PNG?alt=media)
>
> 在这个公式中，`x`代表被赎回的代币数量，`s`代表总代币供应量，`o`代表当前溢出，`r`代表联合曲线利率。

例如：在70%的联合曲线配置下，销毁 10% 的代币供应将能从总溢出中领取到7%左右的ETH，剩下的留给代币持有者共享。

## 怎样创建一个项目？

### 项目详情

- 项目名称
- 项目标识
- 项目说明
- 网站
- Twitter
- Discord
- 支付按钮文本
- 付款声明
  
  文本内容会在您的支持者完成付款前向其显示
- 项目logo

### 筹款周期

筹款周期包含筹款周期持续时间和筹款周期目标。

为了同步治理、支出和项目重新配置，Juicebox项目可以使用“筹款周期”运行。项目所有者不能在资助周期内更改任何项目参数。
您的项目按筹款周期来进行筹款，每个筹款周期都有一个筹款目标和周期时长。您项目的筹款周期配置视您将创建项目的种类而定。

- 筹款周期目标
  - 资金周期目标是每个周期的目标金额。这是每个资金周期可以从Juicebox提取的金额。
  - 设定你每个筹款周期想要筹款的金额。筹款周期目标以内的金额会分配给项目，项目代币持有人不能通过赎回取得这部分资金。
  - 如果您项目的资金余额超出您的筹款周期目标，就会产生溢出。项目代币持有人可以赎回溢出部分资金。
  - 不设定筹款目标。 所有资金都可以分配给项目，项目将不再会产生溢出（把筹款目标设为无限也是同样结果）。

- 筹款周期持续时间
  - 筹款周期持续时间决定了这些资金周期将持续多长时间，并决定了您可以多久提取一次目标金额。
  - 不设定持续时间。可以随时更改筹款配置。更改配置将重新开始一个筹款周期。推荐设置一个持续时间。对于贡献者来说，可以随时修改配置的筹款周期是具有风险的。

没有筹款周期允许项目所有者随时从项目中提取资金，并随时手动触发新的资金周期。在配置资金周期持续时间和资金周期目标时，应考虑您的资金策略（包括贡献者支出和每月固定成本）。

### 资金分发

当项目方从Juicebox金库合约提取资金时，决定资金分配到指定钱包或其它Juicebox上的项目，另外，提取资金时将有5%捐款给JuiceboxDAO，作为平台收入。

把可用资金分发给其他以太坊钱包或者其他Juicebox项目。使用这项功能付款给项目的贡献者、慈善机构、其他帮助你的Juicebox项目、或是任何其他人。无论什么时候从您项目提款，资金都会自动进行发放。

默认的情况下，所有未分配资金可被分发给项目拥有者的钱包。

### 保留代币

当有人对你的项目进行支付时，他们会获得项目代币。在项目设定了筹款目标时, 可以通过赎回项目代币来获得溢出资金。项目合约部署上线后，你就可以铸造ERC-20代币了。在此之后，协议就会开始追踪代币余额，同时允许你的支持者获得代币以及赎回代币取得项目溢出资金。

有人对你的项目付款时，按照设定比例的代币会被保留, 剩余的代币会发送至付款人。在默认情况下, 保留代币会留给项目拥有者, 但是项目拥有者也可以将保留代币分配给其他钱包地址。保留代币产生后，任何人都可以把它们“铸造”出来，亦即把保留代币分发给预先指定的接收人。

### 重新配置

关于如何重新配置该项目筹款周期的规则

推荐设置一个修改配置的策略（延迟生效）。对于贡献者来说，没有策略的项目是具有风险的。

- 策略
  - 延迟3天生效
  - 延迟7天生效
  - 自定义

### 激励措施

激励措施有以下两种设置：

- 折扣率
- 联合曲线比率

### 受限操作

注意：这些属性不能 在同一个筹款周期内马上进行修改。 更改配置只能在 后面的 筹款周期内完成。

- 暂停支付

  暂停期间，你的项目不会再收到直接付款。

- 允许铸造代币
  - 允许项目所有者手动铸造并发送任何数量的代币
  - 允许铸造代币会让捐款人觉得项目有风险，如必非要，请勿使用这个功能。

## 案例分析

### ConstitutionDAO

![ConstitutionDAO](https://i.ibb.co/RCfbkS1/2022-04-02-101418.png)

- 项目详情
- 筹款周期
- 资金分发
- 保留代币
- 重新配置
- 激励措施
- 受限操作

### AssangeDAO

![AssangeDAO](https://i.ibb.co/q1mh0kb/2022-04-02-100134.png)

### JuiceboxDAO

![JuiceboxDAO](https://i.ibb.co/v3wWZ4V/2022-04-02-102340.png)
## 有什么风险？

值得注意的是，一个项目可以在每个融资周期的基础上改变其保留率、筹资目标、赎回联合曲线和折扣率。一些项目可能会选择没有融资周期期限 ，以获得最大的灵活性，这意味着他们可以根据需求重新配置项目。

V2版本并未审计，有漏洞风险，谨慎使用。

相信项目的所有者真的很重要，因为他们有很大的控制权来设定项目的代币经济机制。

例如：项目设置了一个3天延迟的投票合约。如果项目所有者想重新配置任何融资周期的属性，必须在当前融资周期结束前至少3天发送这样的交易请求。

当有人支付 Juicebox 项目时，他们会获得代币奖励。
如果您的项目有资金目标，则收到的任何额外资金都被视为溢出。可以赎回代币以索取一定比例的溢出量。例如，拥有总代币供应量 1% 的钱包可以赎回这些代币以获取 1% 的溢出。
如果启用了允许铸造代币，项目所有者可以向任何钱包铸造任意数量的代币。创建项目后，项目所有者可以使用Juicebox为其项目发行ERC-20代币。未来的付款人将收到ERC-20代币，现有的代币持有者可以根据现有的代币余额申领ERC-20代币。
然后，这些代币可用于连接服务，例如用于脱链投票的snapshot

## Contract Addresses

Addresses and Etherscan links for deployed JB Protocol contracts.

### Juicebox Protocol V1

#### Ethereum Mainnet

TerminalDirectory: [`0x46C9999A2EDCD5aA177ed7E8af90c68b7d75Ba46`](https://etherscan.io/address/0x46c9999a2edcd5aa177ed7e8af90c68b7d75ba46)

TerminalV1: [`0xd569D3CCE55b71a8a3f3C418c329A66e5f714431`](https://etherscan.io/address/0xd569D3CCE55b71a8a3f3C418c329A66e5f714431)

Projects: [`0x9b5a4053FfBB11cA9cd858AAEE43cc95ab435418`](https://etherscan.io/address/0x9b5a4053FfBB11cA9cd858AAEE43cc95ab435418)

TicketBooth: [`0xee2eBCcB7CDb34a8A822b589F9E8427C24351bfc`](https://etherscan.io/address/0xee2eBCcB7CDb34a8A822b589F9E8427C24351bfc)

ModStore: [`0xB9E4B658298C7A36BdF4C2832042A5D6700c3Ab8`](https://etherscan.io/address/0xB9E4B658298C7A36BdF4C2832042A5D6700c3Ab8)

OperatorStore: [`0xab47304D987390E27Ce3BC0fA4Fe31E3A98B0db2`](https://etherscan.io/address/0xab47304D987390E27Ce3BC0fA4Fe31E3A98B0db2)

FundingCycles: [`0xf507B2A1dD7439201eb07F11E1d62AfB29216e2E`](https://etherscan.io/address/0xf507B2A1dD7439201eb07F11E1d62AfB29216e2E)

Active7DaysFundingCycleBallot: [`0xEf7480b6E7CEd228fFB0854fe49A428F562a8982`](https://etherscan.io/address/0xEf7480b6E7CEd228fFB0854fe49A428F562a8982)

Active3DaysFundingCycleBallot: [`0x6d6da471703647Fd8b84FFB1A29e037686dBd8b2`](https://etherscan.io/address/0x6d6da471703647Fd8b84FFB1A29e037686dBd8b2)

Active1DayFundingCycleBallot: N/A

Governance: [`0xAc43e14c018490D045a774008648c701cda8C6b3`](https://etherscan.io/address/0xAc43e14c018490D045a774008648c701cda8C6b3)

Prices: [`0xa9537Cc42555564206D4E57c0eb6943d56E83A30`](https://etherscan.io/address/0xa9537Cc42555564206D4E57c0eb6943d56E83A30)

#### Rinkeby

[https://github.com/jbx-protocol/juice-contracts/tree/main/deployments/rinkeby](https://github.com/jbx-protocol/juice-contracts/tree/main/deployments/rinkeby)

#### Kovan

TerminalDirectory Kovan: [`0x71BA69044CbD951AC87124cBEdbC0334AB21F26D`](https://kovan.etherscan.io/address/0x71BA69044CbD951AC87124cBEdbC0334AB21F26D)

### Juicebox Protocol V2 Rinkeby

JBOperatorStore: [`0x55d4dfb578daA4d60380995ffF7a706471d7c719`](https://rinkeby.etherscan.io/address/0x55d4dfb578daA4d60380995ffF7a706471d7c719)

JBPrices: [`0x47C6072ccDb899C016ED07ae8aEb7b2cfFe3C82e`](https://rinkeby.etherscan.io/address/0x47C6072ccDb899C016ED07ae8aEb7b2cfFe3C82e)

JBProjects: [`0x2B0b6BD05a2F1f2a399F73528a99a495555C4c52`](https://rinkeby.etherscan.io/address/0x2B0b6BD05a2F1f2a399F73528a99a495555C4c52)

JBDirectory: [`0xF77Cc21F7Ffdb0700D6d01FCF32EBE654f1A389b`](https://rinkeby.etherscan.io/address/0xF77Cc21F7Ffdb0700D6d01FCF32EBE654f1A389b)

JBFundingCycleStore: [`0xF77Cc21F7Ffdb0700D6d01FCF32EBE654f1A389b`](https://rinkeby.etherscan.io/address/0xfd6Bc33C9e25c6d9Bbd00b04992E3639E786DCEd)

JBTokenStore: [`0x29431d36f382f50878399C1D529b20582573AAb6`](https://rinkeby.etherscan.io/address/0x29431d36f382f50878399C1D529b20582573AAb6)

JBSplitsStore: [`0xAa818525455C52061455a87C4Fb6F3a5E6f91090`](https://rinkeby.etherscan.io/address/0xAa818525455C52061455a87C4Fb6F3a5E6f91090)

JBController: [`0xd2eEEdB22f075eBFf0a2A7D38781AA320CBc357E`](https://rinkeby.etherscan.io/address/0xd2eEEdB22f075eBFf0a2A7D38781AA320CBc357E)

JBPaymentTerminalStore: [`0x92239434A7d0D17c4d8F876C7DB75E54680Bc85e`](https://rinkeby.etherscan.io/address/0x92239434A7d0D17c4d8F876C7DB75E54680Bc85e)

JBPayoutRedemptionPaymentTerminal: [`0x9d5687A9A175308773Bb289159Aa61D326E3aDB5`](https://rinkeby.etherscan.io/address/0x9d5687A9A175308773Bb289159Aa61D326E3aDB5)
