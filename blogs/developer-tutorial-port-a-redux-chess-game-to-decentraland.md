# Developer Tutorial: Port a Redux Chess Game to Decentraland

# 开发者教程：将 Redux 国际象棋游戏移植到 Decentraland

## Learn how to port a game from Redux into Decentraland using the SDK

## 了解如何使用 SDK 将游戏从 Redux 移植到 Decentraland

![][2]

The Decentraland SDK includes all sorts of hidden gems. One of these is the ability to port existing games and content from other platforms into Decentraland!

Decentraland SDK 包含各种隐藏的"珍宝"。其中之一就是能够将现有游戏和内容从其他平台移植到 Decentraland！

My name is Juan Cazala — I'm part of the dApps crew at Decentraland. We're the team behind the Decentraland Marketplace and the Agora voting platform. If you ever have any feedback for our dApps, you can always reach out to me on Discord!

我叫 Juan Cazala -- 是 Decentraland dApps 工作人员。我们是 Decentraland 虚拟市场和 Agora 投票平台背后的团队。如果您对我们的 dApp 有任何反馈意见，您可以随时通过 Discord 与我联系！

Today, I'd like to teach you how to port a simple chess game from Redux into our SDK so that you can play a live, 3D version of chess right in the metaverse.

今天，我想教您如何将一个简单的国际象棋游戏从 Redux 移植到我们的 SDK 中，这样你就可以在虚拟世界中玩 3D 版的国际象棋。

You can clone the repo that I created for this tutorial by following the [installation guide][3], or you can follow along with each of the steps to recreate the game yourself.

您可以按照[安装指南][3]克隆我为本教程创建的代码库，或者您也可以按照步骤自行重新创建游戏。

Let's get started!

让我们开始吧！

### Porting your Redux game into Decentraland

### 将你的 Redux 游戏移植到 Decentraland

My goal with this tutorial is to show you how you can take an existing Redux game and port it to Decentraland using our SDK. The game I chose to use is [@zackpudil][4]'s [redux-chess-app][5], which looks something like this:

我在本教程中的目标是向您展示如何使用我们的 SDK 将现有的 Redux 游戏移植到 Decentraland。我选择使用的游戏是[@zackpudil][4]的[redux-chess-app][5]，它看起来像这样：

![][7]

#### A quick note on prerequisites

#### 前提说明

This tutorial does assume you are using a unix machine (or at least using a unix-like terminal), with **git**, **npm** and **Decentraland's SDK** installed. If you haven't installed them yet, you can by following these steps:

本教程假设您使用的是 unix 机器（或者至少使用类似 unix 的终端），安装了 **git**，**npm** 和 **Decentraland 的 SDK**。如果您尚未安装它们，可以按照以下步骤操作：
* Install [git][8].

* 安装[git][8]。

* Install [nvm][9] and then run `nvm use stable` to install npm.

* 安装[nvm][9]然后运行 `nvm use stable` 来安装 npm。

* Once you have npm installed, run `npm install -g decentraland` to install Decentraland's SDK.

* 一旦安装了 npm，运行 `npm install -g decentraland` 来安装 Decentraland SDK。

#### Want to fast-forward through some of my steps?

#### 想快进我的一些步骤吗？

Each step in this tutorial is represented by [its own release][10] in the tutorial's repo, so you can fast-foward to any step using `git clone`, like this:

本教程中的每一步都由教程的代码库的[发行版][10]表示，所以你可以使用 `git clone` 快进到任何步骤，如下所示：

git clone --branch step-0  --depth=1

Just replace the `**step-0**` with the step number you want to jump to.

只需将 `**step-0**' 替换为您要跳转到的步骤编号。

### Step 0: Initialize your scene

### 步骤0：初始化场景

The first step is to clone the repo from the original Redux game that we want to work with:

第一步是克隆我们想要使用的原始 Redux 游戏中的代码：

```
git clone https://github.com/zackpudil/redux-chess-app
cd redux-chess-app
```

Then, install its dependencies by running the following command from the repo's folder:

然后，通过从 repo 的文件夹运行以下命令来安装其依赖项：

```
npm install
```

Now we can initialize our Decentraland scene in a folder inside this same repo. We'll create a scene directory and initialize the SDK in it:

现在我们可以在同一个repo 内的文件夹中初始化我们的 Decentraland 场景。我们将创建一个场景目录并在其中初始化SDK：

```
mkdir scene
cd scene
dcl init
```

The SDK will prompt you with a few questions in order to initialize the scene. It will ask you which type of scene is this going to be. **Make sure you select "Remote"** (the third option).

SDK 会提问一些问题，以便初始化场景。它会问你哪种类型的场景。 **确保选择“Remote”**（第三个选项）。

It will also ask you which parcel(s) comprise this scene. If you don't have any parcels that's okay, you can enter any coordinates like **0,0** since we are running this scene locally and you don't need to own any LAND to build and preview scenes using the SDK.

它还会询问您使用哪个地块构成此场景。如果您没有土地，也没关系，您可以输入任何坐标，例如 **0,0**，因为我们在本地运行此场景，您不需要拥有任何LAND 来使用 SDK 构建和预览场景。

Now that we have initialized our scene, we are (almost) ready to start porting the game.

现在我们已经初始化了我们的场景，我们（几乎）已准备好可以开始移植游戏。

First, we need to replace the _aliased_ imports with _relative_ ones, because the former are not compatible with Decentraland's SDK, like this:

首先，我们要将 import 中的别名替换成相对路径，因为前者与 Decentraland 的 SDK 不兼容，如下所示：

If you don't want to deal with replacing all of those aliases, and just want to jump into the fun stuff, you can skip this step by running the fast-forward command from below:

如果您不想处理替换所有这些别名，并只想跳转到有趣的地方，您可以运行以下行快进命令跳过此步骤：

**Diff: **To see the full diff of changes for this step check [this commit][12].

**Diff：** 要查看此步骤的完整差异，请看[此提交][12]。

**Fast-Forward:** to jump to the end of this step, run:

**快进：** 跳到此步骤结束，运行：


git clone --branch step-0  --depth=1

git clone --branch step-0 --depth = 1

### Step 1: Port your game to the Decentraland scene

### 步骤 1：将游戏移至 Decentraland 场景

Now we can start porting the chess game to our scene. Inside the scene directory that we created during the previous step, you'll find a server folder. Let's navigate into that folder:

现在我们可以开始将国际象棋游戏移植到我们的场景中。在我们在上一步中创建的场景目录中，有一个 server 文件夹，进入该目录​​：


cd server


We can start by deleting the `State.ts` file, since the game state will now reside in the Redux store.

让我们开始吧，删除`State.ts`文件，因为游戏状态现在将驻留在 Redux store。


rm State.ts

rm State.ts

Now let's add a `Store.ts` file where we will import the `redux` store, initialize it, and then export it with all of the actions that we will use in our new Decentraland scene:

现在让我们添加一个 `Store.ts` 文件，我们将导入 `redux` 存储，初始化它，然后将新的 Decentraland 场景中需要使用的所有操作导出：

We need to modify `ConectedClient.ts` so that all of the clients get updated when there's a change in the Redux store:

我们需要修改 `ConectedClient.ts`，以便 Redux 存储中发生更改时更新所有客户端：

We can now create an `assets` folder inside our `scene` directory to place the models for all the pieces:

然后在 `scene` 目录下创建一个 `assets` 文件夹来放置所有模型：


cd ..

cd ..
mkdir assets

(If you want, you can find all of these assets [here][13].)

（如果你愿意，你可以在[这里][13]找到所有这些资产。）

Once all the models have been placed in the `assets` folder we can back up to the server's folder:

一旦所有模型都放在 `assets` 文件夹中，我们就可以备份到服务器的文件夹：


cd ..

cd ..
cd server

Finally, we need to modify `RemoteScene.tsx` so that it imports the Redux store, gets its state, and uses that state to render the board and all of the pieces in the scene.

最后，我们需要修改 `RemoteScene.tsx`，以便它导入 Redux 存储，获取其状态，并使用该状态来渲染板和场景中的所有部分。

Let's start by removing the import of `State.ts` and replace it with `Store.ts`

让我们首先删除导入的 `State.ts` 并用`Store.ts` 替换

Now let's replace the `render` function with the following:

现在让我们用以下代码替换 `render` 函数：

This will render the output of the `renderBoard` method. Let's define this method:

使用了 `renderBoard` 方法的输出来 render。我们来定义这个方法：

That will render a base entity and position it on the scene, then it will get the `squares` array from the Redux store's state and run a `map` operation over it, running the `renderSquare` method for each square.

这将呈现一个基本实体并将其放置在场景上，然后它将从 Redux 商店的状态获取 `squares` 数组并对其进行 `map` 操作，为每个方块运行`renderSquare` 方法。

This method will receive each `square` and its index (which goes from 0 to 63). Each `square` contains the state for a particular tile on the board. The state indicates:

这个方法将接收每个 `square` 及其索引（从 0 到 63）。每个 `square` 包含棋盘上特定块的状态。该状态表示：

* If there's a chess piece on the tile, and which piece that is

* 如果特定格子上有棋子，那是哪一个格子

* If the tile is selected

* 有没有选择这个格子

* If the tile is highlighted

* 格子有没有突出显示

* If the tile is in check

* 格子是否被将军
  
We can then use this information to render the board on the scene.

然后，我们可以使用这些信息在场景中显示棋盘。

The first thing we need to do is convert the 1-dimensional index (0 to 63) into 3D coords (x, y, z).

我们需要做的第一件事是将1维索引（0 到 63）转换为 3D 坐标（x，y，z）。

The second thing we have to do is figure out the color of the tile, which will alternate between black and white, unless the tile is in a special state (highlighted, selected, or in check):

我们要做的第二件事是弄清楚特定格子的颜色，它将在黑色和白色之间交替，除非特定格子处于一种特殊状态（突出显示，选中或将军）：

* If the square is selected, we make it _green_.

* 如果正方形被选中，我们将其设为 _green_。

* If the square is highlighted, we compare the `pieceId` with the string `'_'` (which means there's no chess piece on that square).

* 如果正方形突出显示，我们将 `pieceId` 与字符串''_'`进行比较（这意味着该正方形上没有棋子）。

* If there are no pieces on the square, the player can move to it, so we make it _yellow_.

* 如果正方形上没有棋子，玩家就可以移动到此位置，所以我们设为 _yellow_。

* If there's a piece on the square, the player can eat it, so we make it _red_.

*如果正方形上有棋子，玩家可以吃掉它，所以我们将它设为 _red_。
* If the square is in check we will make it _orange_.

* 如果此正方形被将军，我们设为 _orange_。

Before rendering the actual tile, let's add a `modelsById` map at the top of our file that maps each `pieceId` to the corresponding model, like this:

在呈现实际格子之前，让我们在文件顶部添加一个名为 `modelsById` 的map 集合，将每个 `pieceId` 映射到相应的模型，如下所示：


Now we can write the last part of the `renderSquare` method:

现在我们可以编写 `renderSquare` 方法的最后一部分：


For each square, we are rendering an `<entity>` as a wrapper in its corresponding position, inside this entity we render a `<box>` that represents the tile. If the `square.pieceId` is inside our `modelsById` map, we also render a `<glft-model>` that represents the piece.

对于每个正方形，我们在其对应的位置呈现一个作为包装器的 `entity` ，在这个实体中我们呈现一个表示棋盘格子的`<box>`。如果 `square.pieceId` 在我们的 `modelsById` 映射中，我们还会显示 一个 `<glft-model>` 用于显示棋子。

We need to add `id`s to both the `<box>` and the `<gltf-model>`.

我们需要在 `<box>` 和 `<gltf-model>` 中添加 `id`。

**In order to listen for a click event on an entity, the entity must have its own id.**

**为了监听实体上的 click 事件，实体必须拥有自己的 id。**

To listen for events we need to modify the `eventSubscriber` that was created as part of the default scene, let's start by removing the call to `setState`:

对监听事件，我们需要修改作为默认场景一部分创建的 `eventSubscriber`，让我们首先删除对 `setState` 的调用：


We can get the `elementId` from the `event` object that receives the listener:

我们可以从监听器接收的 `event` 对象中获取 `elementId`：


That `elementId` can have either a `-tile` suffix or a `-piece` suffix. We need to get the `squareId` from that `elementId`by removing the suffix. Let's add this helper function at the top of the file:

`elementId` 可以有 `-tile` 后缀或 `-piece` 后缀。我们需要通过删除后缀从 `elementId` 获取 `squareId`。让我们在文件顶部添加这个帮助函数：


This expression takes the string from `elementId`, splits it in two at the `-` character, and returns the first part. Let's use it to get the `squareId` and dispatch a `squareClick` action:

此表达式从 `elementId` 获取字符串，在 `-` 处将其拆分为两个，并返回第一部分。让我们用它来获取 `squareId` 并发送一个 `squareClick` 动作：


Now we are all set!

现在我们都准备好了！

Let's run a build for the server and test out what we have so far:

让我们构建服务并测试我们到目前为止的内容：


npm run build
npm start

That will start our server, which we must keep running. On a second terminal window, go to the `scene` directory and start the SDK preview:

这将启动我们的服务器，它将一直运行。在第二个终端窗口，转到 `scene` 目录并启动 SDK 预览：


cd ..
dcl preview

From your web browser, open `http://localhost:8000` and you should see the board rendered on the screen, you should be able to click on the piece to move them, in the same way as in the original game!

在浏览器中，打开 `http://localhost:8000`，您应该会看到屏幕上的棋盘，并且可以点击棋子来移动，就像在原始游戏中一样！

![][15]

**Diff:** to see the full diff of changes for this step check [this commit][16].

**Diff：** 查看此步骤的完整修改[this commit][16]。

**Fast-Forward:** to jump to the end of this step run `git clone --branch step-1 https://github.com/cazala/decentraland-redux-chess-app.git --depth=1`

**快进：** 直接跳到这一步 `git clone --branch step-1 https://github.com/cazala/decentraland-redux-chess-app.git --depth = 1 `

### Step 2: Supporting multiple players!

### 步骤2：支持多个玩家！

It's no fun to play chess by yourself, so in this last step we will modify the server so that it:

自已跟自己下棋是没有意思的，所以在最后一步中我们将修改服务器：

* Keeps track of which clients are playing

* 跟踪哪些客户在玩

* Keeps track of the status of the match

* 跟踪比赛的状态

* Only lets the clients who are currently playing move the pieces

* 只允许当前在玩的客户移动棋子

* Only let clients move their own pieces

* 只允许客户移动他们自己的棋

So the first thing we will do is add a `match` module to the redux game, under `src/modules/match`.

所以我们要做的第一件事是在 `src/modules/match` 下为 redux 游戏添加一个 `match` 模块。

In that new module, let's add three actions: `registerPlayer`, `unregisterPlayer` and `checkmate`:

在这个新模块中，让我们添加三个动作：`registerPlayer`，`unregisterPlayer` 和 `checkmate`：


Let's add a reducer to handle those actions:

让我们添加一个 reducer 来处理这些动作：

In this section of the state, we will keep track of the game `status.`The game status can be either `idle`, `started` or `checkmate`. We will also store the `id` of the clients that are using either the black pieces or the white ones. Below we will see how to handle each of the possible actions. We'll start by the action of resetting to the initial state, which is already defined:

在 state 这一部分，我们将跟踪游戏的状态 `status.` 。游戏状态可以是`idle` - 空闲，`started` - 开始 或 `checkmate` - 将死。我们还将存储使用黑棋或白棋的用户的 `id`。下面我们将看到如何处理每个可能的操作。我们将从重置为初始状态的操作开始，该状态已经定义：


case INIT_SQUARES:

return initialState

The `INIT_SQUARES` action is quite simple, it just resets the state to its default values.

`INIT_SQUARES` 动作非常简单，它只是将状态重置为默认值。

Let's look at the action required to add a new player into the game:

让我们看一下将新玩家添加到游戏中所需的操作：


* If both players are already registered, we will ignore this action.

* 如果两个玩家都已注册，我们将忽略此操作。

* If this player id is already registered as the white or the black player, we will also ignore this action.

* 如果此玩家 ID 已经注册为白棋或黑棋，我们也会忽略此操作。

We then check the value of `action.isWhite` to find out which color to register the new client with. Once there are two clients registered, with each one assigned to a color, we change the `status` to `started`.

然后我们检查 `action.isWhite` 的值，找出用户注册的颜色。一旦有两个用户注册，每个用户分配一个颜色，我们将 `status` 更改为 `started`。

That's all we have to do to register the players for the game. Now, let's see how to unregister them:

这就是我们为游戏注册玩家所需要做的一切。现在，让我们看看如何取消注册：

We simply check if the client that wants to unregister is one of the two active players, and if so, we reset the entire game to the `idle` state.

我们只要检查想要取消注册的用户是否是两个活跃玩家中的一个，如果是，我们将整个游戏重置为 `idle` 状态。

Finally, we handle the "checkmate" action:

最后，我们处理“将死”操作：


So, now our server is capable of registering which players are currently playing. We can plug this new reducer into our store (this is `src/store`):

所以，现在我们的服务器能够注册当前正在游戏的玩家。我们可以将这个新的 reducer 插入我们的 store（这是 `src/store` ）：

The last thing we need to do on the Redux side is to modify the `Analysis Middleware` to handle the "checkmate" action:

我们在 Redux 方面需要做的最后一件事是修改 `Analysis Middleware`来处理 “checkmate” 动作：

Basically, this code checks to see if the king is in check. If it is, we filter all squares with pieces from the player who is in check:

基本上，这段代码会检查国王是否将军。如果是，我们过渡被将军的玩家所有的有棋子的格子。

Then we run our game engine on each of those squares, and compute the amount of valid moves that the player has left:

然后我们在每个格子上运行我们的游戏引擎，并计算玩家剩下的有效移动数量：

If the amount of valid moves is 0, then we know the player is in checkmate, so we can dispatch a `checkmate()` action, followed by a game reset 10 seconds later:

如果有效移动的数量为0，那么我们知道玩家处于将死状态，因此我们可以发出 `checkmate()` 动作，然后在 10 秒后重置游戏：

That wraps up everything we had to do on the Redux side! Let's go back to the server in (`scene/server`) and modify the `Server.ts` file so that it dispatches an `unregisterPlayer()` action when a client disconnects:

这包含了我们在 Redux 方必须做的一切！让我们回到（`scene/server`）服务器并修改 `Server.ts` 文件，以便在客户端断开连接时处理`unregisterPlayer（）`动作：

Finally, we need to modify `RemoteScene.tsx` to handle both game states (`game started` and `idle`), allow user registration, and prevent users from playing when it's not their turn.

最后，我们需要修改 `RemoteScene.tsx` 以处理游戏状态（“游戏开始”和“空闲”），允许用户注册，并防止用户在没有轮到他们时进行游戏。

The first thing we need to do is to add an `id` to each client (this will be used as the player id). Let's generate this id randomly:

我们需要做的第一件事是向每个客户端添加一个 `id`（这将被用作玩家 ID）。让我们随机生成这个 id：


Now let's replace the `render` method with the following:

现在让我们用以下代码替换 `render` 方法：


That will read the game `status` from the Redux store and render either the `idle` state or the board.

这将从 Redux store 读取游戏 `status` 并显示 `idle` 状态或棋盘。

We can now define what we render when the scene is idle in `renderIdle()`. We will render a white queen and a black queen on the scene, and some text that reads "Choose your color".

我们现在可以在 `renderIdle()` 中定义场景空闲时渲染的内容。我们将在场景中显示一个白色王后和一个黑色王后，还有一些文字写着 “选择你的颜色”。

We will assign the ids `register-white` and `register-black` to the queens so we can listen to click events on them. When any of the players is registered, we will render that queen in the position `y: 1` (elevated up in the air) to indicate that it has already been selected by another player:

我们将把 ids `register-white` 和 `register-black` 分配给皇后，这样我们就可以监听到它们上的点击事件。当任何一个玩家注册时，我们会将该女王显示在 `y：1` 的位置（在空中升起）以表明它已经被另一个玩家选中：

Now we only need to modify the `eventSubscriber` to dispatch the register actions, and to prevent dispatching click actions when it's not the player's turn.

现在我们只需要修改 `eventSubscriber` 来响应注册动作，并防止在没有轮到玩家时响应点击动作。

First, we will read whose turn it is (black or white) and both player ids from the state:

首先，我们将从 state 中读取轮到谁（黑色或白色）和两个玩家的 ID：


Now we can check to see either of the two "register" queens have been clicked on, and if so, dispatch a `registerPlayer`action. The first player who registers will also dispatch an `initSquares` to reset the board from any previous games:

现在我们可以检查是否已经点击了两个“注册”皇后中的任何一个，如果是，则调用 `registerPlayer`。注册的第一个玩家也将发送一个`initSquares` 来重置棋盘：

Finally, if the `elementId` doesn't match any of the "register" queens, we can dispatch a `squareClick` event, but only after checking that it is this client's turn:

最后，如果 `elementId` 与任何“注册”的皇后都不匹配，我们可以调用一个 `squareClick` 事件，但只有是在轮到这个玩家之后：

Finally let's add a `` that lets the players know whose turn it is, and announces when there's a "checkmate".

最后让我们添加一个 `<text>` 让玩家知道轮到谁走，并在”将死“后宣布。

For this, we will add a `renderMessage` method and call it from `renderBoard`:

为此，我们将添加一个 `renderMessage` 方法并从 `renderBoard` 调用它：

Let's define `renderMessage` using the following:

让我们使用以下内容定义 `renderMessage`：


That's all there is to it!

这样就全好了！

Now, two players can start a match and play against each other. Any other connected client will be able to see the game, but they won't be able to move any of the pieces:

现在，两名参赛人员可以开始一场比赛。任何其他连接的客户将能够看到游戏，但他们无法移动任何棋子：

Remember that after making any changes to the code you will need to re-build your server and restart it:

请记住，在对代码进行任何更改后，您需要重新构建并重新启动服务器：


npm run build

npm start


**Diff:** to see the full diff of changes for this step check [this commit][19].

** Diff：** 查看此步骤的所有修改[this commit][19]。

**Fast-Forward:** to jump to the end of this step run `git clone --branch step-2 https://github.com/cazala/decentraland-redux-chess-app.git --depth=1`

**快进：** 跳到这一步运行 `git clone --branch step-2 https://github.com/cazala/decentraland-redux-chess-app.git --depth=1`

Thank you for following along with this tutorial! I hope that it's helped to show you how easy it is to port simple Redux games into the Decentraland SDK, opening up even more options that you can use your LAND for.

感谢您关注本教程！我希望有助于向您展示，将简单的 Redux 游戏移植到Decentraland SDK 中是多么容易，让你对 LAND 用途有更多选择。

**Don't forget to check out some of our other developer tutorials:**

**不要忘记查看其他开发人员教程：**

* [Build Your First Interactive Scene Using the SDK][20]

* [使用 SDK 构建您的第一个交互式场景][20]
  
* [Building a Memory Game Using Decentraland's SDK][21]

* [使用 Decentraland 的 SDK 构建记忆游戏][21]

### Join the conversation

### 加入对话

* [Discord][22]

* [Twitter][23]

* [Reddit][24]

* [Telegram][25]

* [Get started with the SDK!][26]


[1]: https://cdn-images-1.medium.com/freeze/max/60/1*0r-9jJtFak1GgM2vrg8LVw.png?q=20
[2]: https://cdn-images-1.medium.com/max/2000/1*0r-9jJtFak1GgM2vrg8LVw.png
[3]: https://github.com/cazala/decentraland-redux-chess-app#installation
[4]: https://github.com/zackpudil
[5]: https://github.com/zackpudil/redux-chess-app
[6]: https://cdn-images-1.medium.com/freeze/max/60/0*CkmIU8Kv0LotDc7g?q=20
[7]: https://cdn-images-1.medium.com/max/1600/0*CkmIU8Kv0LotDc7g
[8]: https://git-scm.com/book/en/v1/Getting-Started-Installing-Git
[9]: http://nvm.sh/
[10]: https://github.com/cazala/decentraland-redux-chess-app/releases
[11]: https://i.embed.ly/1/display/resize?url=https%3A%2F%2Favatars2.githubusercontent.com%2Fu%2F2781777%3Fs%3D400%26v%3D4&key=a19fcc184b9711e1b4764040d3dc5c07&width=40
[12]: https://github.com/cazala/decentraland-redux-chess-app/commit/8338a8d99332ae555ce786110480133cd621e9b9
[13]: https://github.com/cazala/decentraland-redux-chess-app/tree/master/scene/assets
[14]: https://cdn-images-1.medium.com/freeze/max/60/0*9z2uhl5o9q6HAOK9.gif?q=20
[15]: https://cdn-images-1.medium.com/max/1600/0*9z2uhl5o9q6HAOK9.gif
[16]: https://github.com/cazala/decentraland-redux-chess-app/commit/61f4ae3a8bb0b0a4095fd052f11f846b9c199864
[17]: https://cdn-images-1.medium.com/freeze/max/60/0*gOzrYM321wkI5G4u.gif?q=20
[18]: https://cdn-images-1.medium.com/max/1600/0*gOzrYM321wkI5G4u.gif
[19]: https://github.com/cazala/decentraland-redux-chess-app/commit/d67179baa87962cdef6de65835bf4e43418de1fa
[20]: https://blog.decentraland.org/build-your-first-interactive-scene-using-the-sdk-5d6895ac78f0
[21]: https://blog.decentraland.org/building-a-memory-game-using-decentralands-sdk-87ee35968f8d
[22]: https://discordapp.com/invite/9EcuFgC
[23]: https://twitter.com/decentraland
[24]: https://www.reddit.com/r/decentraland/
[25]: https://t.me/decentralandTG
[26]: https://developers.decentraland.org/



from: https://blog.decentraland.org/developer-tutorial-port-a-redux-chess-game-to-decentraland-49f509b2eba6
