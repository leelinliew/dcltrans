
# Decentraland Project Update — July 17th

# Decentraland项目更新 -  7月17日

## News and updates from Decentraland

## 来自 Decentraland 的新闻和更新

![][2]

We have a few bits of news to share with you since our last Project Update.

自上次项目更新以来，我们有一些消息将要与您一起分享。

There's a new endpoint in the LAND API that we want to share, we're still making progress with the Estates feature, we've made some changes to the CLI and how it handles validations when initializing a new project, and we've made a few small changes to Agora's styling.

LAND API 加入了新的功能，我们在地产（地块组合买卖）功能上也取得了一些进展，对 CLI 进行了一些更改，加入了初始化新项目时验证处理功能，我们对 Agora 界面做了一些小改动。

Finally, we want to share a few of the bounties that we're hosting on GitCoin.

最后，我们想分享一些我们在 GitCoin 上主办的一些奖励。

### Updates in the Marketplace

### 虚拟市场的更新

First off, our dApps team released [version 0.11.4 of the Marketplace][3] last week, which mostly included smaller patches and fixes.

首先，我们的 dApps 团队上周发布了[虚拟市场 0.11.4 版本][3]，其中主要包括小补丁和修复程序。

More notably, we've added a new `**GET /map**` endpoint to the LAND API, which returns all of the parcels in a given area (including any Estates, once the feature is launched). For details on how to use the `/map` endpoint, [check out our docs][4]!

更值得注意的是，我们在 LAND API 中添加了一个新的`**GET /map **` 功能，它返回给特定区域中的所有地块（也包括所有的地产，一旦该功能启动）。有关如何使用`/ map` 的详细信息，[查看我们的文档][4]！

We're still making progress with Estates. Last week, we began work on converting Estates into fully-fledged ERC 721 tokens, complete with composable properties.

我们在地产取得了一些进展。上周，我们开始致力于将地产转换为完全成熟的 ERC 721 通证，并具有可组合的特性。

### Agora is now two weeks old!

### Agora 出生两周了！

Since Agora was launched two weeks ago, it has processed 368 votes across 29 different polls, with zero downtime! We're super excited that it's being put to use by the Community Districts. Since the initial launch, we've made a few small changes to the styling of the app that you may have noticed.

自两周前推出 Agora 以来，已经处理了 29 个不同投票，共投了 368 票，零停机时间！我们非常兴奋，因为它正在被小区使用。自首次推出以来，您可能注意到我们对应用程序界面进行了一些小小的更改。

Don't forget to reach out to us on [Discord][5] if you have any questions or run into any issues when using Agora.

如果您在使用 Agora 时遇到任何问题，请不要忘记在[Discord][5]上与我们联系。

### Updates in the SDK

### SDK 更新

Last week, we released a few small changes improving the developer experience of the CLI.

上周，我们发布了一些小改动，改善了 CLI 开发人员的体验。

There is now a new validation process that will run each time you initialize a new project. The CLI will check to ensure that your scene doesn't extend beyond your parcel's boundaries, it will protect you from overwriting any existing or conflicting data, and finally it will run some security and ownership validations. Our goal is to help you save time by catching any mistakes you may have made as soon as possible.

现在有一个新的验证过程，会在每次初始化新项目时运行。 CLI 将检查以确保您的场景不会超出您的地块边界，它将保护您不会覆盖任何现有或冲突的数据，最后它将进行一些安全性和所有权验证。我们的目标是通过尽快发现您可能犯的任何错误，来帮助您节省时间。

We've also begun work on the default user interface in the Decentraland Client, resolving a few performance issues along the way. A big component of the Client UI that we're tackling now is the communications layer, or the features and interface allowing users in the same scene to interact with each other.

我们还开始 Decentraland Client 默认用户界面开发，解决了一些性能问题。我们现在要处理的客户端 UI 的一个重要组成部分是通信层，或者允许同一场景中的用户相互交叉的功能和界面。

### Decentraland Bounties

### Decentraland Bounties

[We've recently begun listing bounties on GitCoin][6] to help incentivize content creation within the Decentraland community.

[我们最近开始在 GitCoin 上列出奖金][6]，以鼓励 Decentraland 社区内的内容创建。

Right now we have several bounties offering MANA for individuals interested in writing guest blog posts (you could have your writing featured right on the Decentraland blog!), producing video tutorials for the SDK, and organizing meetups for game developers interested in the Decentraland SDK.

现在我们为有兴趣撰写博客帖子的人提供 MANA 奖励（你可以在 Decentraland 博客上发表你的作品！），为 SDK 制作视频教程，及组织对 Decentraland SDK 感兴趣的游戏开发者聚会。

For more details about each of these bounties, with instructions on how to apply, [check out our profile on GitCoin!][6]

有关这些奖励的详细信息，以及如何申请的说明，[查看我们在 GitCoin 上的介绍！][6]

### NIFTY is just a few days away!

### NIFTY 就在几天之后！

We're getting extremely excited for the [upcoming NIFTY conference and hackathon][7] in Hong Kong! With just less than a week to go, we can't wait to kick off the first conference dedicated to non-fungible tokens and blockchain-based gaming.

我们对在香港即将召开的 NIFTY 会议和黑客马拉松感到非常兴奋！距离还有不到一周的时间，我们迫不及待地召开了第一次会议，专门讨论非同质通证和基于区块链的游戏。

Leaders in blockchain tech and online gaming are traveling to Hong Kong from around the globe to discuss the intersection of these two exciting industries. In addition to the lineup of talks and presentations, NIFTY will be hosting the very first blockchain gaming hackathon.

区块链技术人员和在线游戏的领导者正从全球各地前往香港，讨论这两个令人兴奋的行业的交汇点。除了会谈和演示之外，NIFTY 还将举办第一届区块链游戏黑客马拉松。

Visit [**nifty.gg**][7]** **to grab your tickets and to browse through the agenda!

请访问 [**nifty.gg**][7] 获取门票并浏览会议议程！


[1]: https://cdn-images-1.medium.com/freeze/max/30/0*kDPzIDEVcs7IbqdS?q=20
[2]: https://cdn-images-1.medium.com/max/2000/0*kDPzIDEVcs7IbqdS
[3]: https://github.com/decentraland/marketplace/releases/tag/0.11.4
[4]: https://docs.decentraland.org/decentraland/api/#map
[5]: https://discordapp.com/invite/9EcuFgC
[6]: https://gitcoin.co/profile/decentraland
[7]: https://www.nifty.gg/
[8]: https://twitter.com/decentraland
[9]: https://www.reddit.com/r/decentraland/
[10]: https://t.me/decentralandTG
[11]: https://developers.decentraland.org/

