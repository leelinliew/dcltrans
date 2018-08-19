
# Decentraland Project Update — August&nbsp;14th

# Decentraland 项目更新 -  8月14日

## News and updates from Decentraland

## 来自 Decentraland 的新闻和更新

![][2]

It's time for another project update from Decentraland! We have a handful of exciting changes and additions in both the SDK and the Marketplace that we want to fill you in on.

又到了 Decentraland 项目更新的时候了！我们在 SDK 和虚拟市场中更改和添加了一些令人兴奋的功能，并希望您参与。

We've renamed a few of our packages in the SDK, we've added support for Ledger hardware wallets with the CLI, and we've improved the process of linking your 3D content with your LAND.

我们在 SDK 中重新命名了一些软件包，并且在 CLI 中添加了对 Ledger 硬件钱包的支持，我们还改进了将您的 3D 内容与 LAND 的链接的过程。

In the Marketplace, we've fixed some querying errors in the API, we're making progress with LAND Estates, and we are almost finished translating the entire dApp into Japanese.

在虚拟市场中，我们修复了 API 中的一些查询错误，并在 LAND 地产功能上取得了进展，并已经几乎完成整个 dApp 的日语翻译。

### SDK

### SDK

We've made a few changes to the Decentraland SDK since our last project update. You might have already noticed that a couple of our packages are renamed:

自上次项目更新以来，我们对 Decentraland SDK 进行了一些更改。您可能已经注意到我们的一些软件包已重命名：

* **metaverse-api **is now **decentraland-api**

* **metaverse-api** 现改为 **decentraland-api**

* **metaverse-rpc **is now** decentraland-rpc**

* **metaverse-rpc** 现改为 **decentraland-rpc**

* **metaverse-compiler** is now **decentraland-compiler**

* **metaverse-compiler** 现改为 **decentraland-compiler**

The SDK now also supports an `**onClick**` event for entities. This new event type should make it much easier to program interactive scenes.

SDK 现在还支持实体的 `** onClick **` 事件。这种新的事件类型可以大大方便交互式场景的开发。

There are also a few other changes to the CLI, the most notable of which is the addition of Ledger hardware wallet support.

CLI 还有其他一些变化，其中最值得注意的是增加了对 Ledger 硬件钱包的支持。

If you use a Ledger hardware wallet with your LAND, you can now execute `**dcl deploy --https**` instead of `**dcl deploy**` command to link the changes in your parcel with your LAND. The addition of the `**\--https**` flag ensures that when your browser is opened to carry out the transaction, it serves a website with a self-signed **https** certificate (the Ledger web integration requires a secure http connection).

如果您使用带有 LAND 的 Ledger 硬件钱包，您现在可以执行 `**dcl deploy --https**` 而不是 `**dcl deploy**` 命令来更改您的地块的链接。添加的 `**\--https**` 可确保打开您的浏览器以执行交易时，它会为具有自签名 **https** 证书的网站提供服务（Ledger Web 集成需要安全的 http 连接）。

Currently, the certificate is self-signed, so your browser might give you a warning before launching the page. Don't worry, it's still safe to continue! The warning is displayed only because the certificate is self-signed by your machine.

目前，证书是自签名的，因此您的浏览器可能会在打开页面之前向您发出警告。别担心，这是安全的！显示警告只是因为证书是由您的机器自签名的。

Metamask has also recently added support for Trezor hardwallets, so Trezor, Ledger, and Metamask users can all link the content from their parcels with their LAND.

Metamask 最近还增加了对 Trezor 硬件的支持，因此 Trezor，Ledger 和 Metamask 用户都可以将他们的地块内容与他们的 LAND 链接起来。

Finally, The CLI's linker dApp has been updated to use our **decentraland-dapps** library, which is [fully documented and available here][3]. The CLI now also ensures that the linking process is closed only after your transaction has been completed successfully. This should remove any confusion when linking your content to your LAND.

最后，CLI 的链接器 dApp 已更新为使用我们的 **decentraland-dapps** 库，它具有[完整的文档并可在此处获得][3]。 CLI 目前只有在确保交易成功完成后才会关闭链接过程。这样可以消除将内容链接到 LAND 时产生的一些困惑。

### Marketplace &amp;&nbsp;dApps

### 虚拟市场 & dApps

Our Marketplace and dApps team has been hard at work to improve the UX the Marketplace. Most recently, they resolved a few minor issues that users were encountering when querying results through the LAND API.

我们的虚拟市场和 dApp 团队一直在努力改进用户体验。最近，他们解决了用户在通过 LAND API 查询结果时遇到的一些小问题。

They are also making good progress toward releasing the LAND Estates feature, which will allow users to group parcels of LAND together to simplifying deploying large scenes, and buying or selling multiple parcels at once. They've finished the front end development, are continuing to test the integration on the Ropsten network, and are in the middle of conducting an external audit. The Estate smart contract is now also upgradeable via the ZepplinOS!

他们在发布 LAND 地产功能方面也取得了很大进展，地产功能允许用户将 LAND 的地块组合在一起，来简化部署大型场景，或同时购买或出售多个地块。他们完成了前端开发，正在继续进行 Ropsten 网络集成测试和外部审计。 地产的智能合约现在也可以通过 ZepplinOS 升级！

This week, we're adding a small feature to the Marketplace targeted toward developers. Currently, whenever you deploy new parcel content from the CLI, a link is sent to IPFS tying your new content to your LAND token. Once deployed, this new feature will allow you to edit that link directly from the Marketplace's page for your parcel.

本周，我们向面向开发人员的虚拟市场添加了一个小功能。目前，无论何时从 CLI 部署新的地块内容，都会向 IPFS 发送一个链接，以将新内容绑定到 LAND 通证。部署后，此新功能将允许您从虚拟市场您的土地页面直接编辑该链接。

**Please heed the warning by this field! Changing the URL in the "Parcel content link" field changes the content hosted on your LAND.**

**请注意这个字段的警告！更改“土地内容链接”字段中的 URL 会更改您的 LAND 上托管的内容。**

![][6]

Finally, we're working on translating our LAND Marketplace into Japanese to make the application as accessible as possible to our users in Japan.

最后，我们正在努力将土地虚拟市场翻译成日语，以尽可能方便日本用户访问应用程序。


[1]: https://cdn-images-1.medium.com/freeze/max/60/0*LGXwpx0LUm4_5g19?q=20
[2]: https://cdn-images-1.medium.com/max/2000/0*LGXwpx0LUm4_5g19
[3]: https://github.com/decentraland/decentraland-dapps
[4]: https://cdn-images-1.medium.com/freeze/max/60/0*2VYcS1H5PhUXJ-Fc?q=20
[5]: https://blog.decentraland.org/undefined
[6]: https://cdn-images-1.medium.com/max/1600/0*2VYcS1H5PhUXJ-Fc
[7]: https://discordapp.com/invite/9EcuFgC
[8]: https://twitter.com/decentraland
[9]: https://www.reddit.com/r/decentraland/
[10]: https://t.me/decentralandTG
[11]: https://developers.decentraland.org/

