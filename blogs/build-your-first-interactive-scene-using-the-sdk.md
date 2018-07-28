
# Developer Tutorial: Build Your First Interactive Scene Using the SDK

# 开发人员教程：使用 SDK 构建您的第一个交互式场景

## Learn how to use the SDK to build a dynamic, interactive scene that responds to user-generated events

## 了解如何使用 SDK 来创建响应用户事件的动态交互式场景

![][2]

Most people use virtual worlds for what's called "dollhousing", or gathering a bunch of stuff that looks nice or says something about you, and then showing it off to other users. However, the Decentraland SDK has so much more to offer.

大多数人将虚拟世界当成所谓的“玩具屋”，或者把它做为一个收集一堆看起来不错或与你有关的的东西，然后将它向其他用户展示的地方。但是，Decentraland SDK 提供了更多功能。

My name is Nicolas Earnshaw, and I take care of the Decentraland documentation, that means everything you can find in [docs.decentraland.org][3]. If you have any feedback on our docs, please make a pull request or create an issue on the [docs GitHub repo][4]!

我是 Nicolas Earnshaw，负责处理 Decentraland 文档，即[docs.decentraland.org][3]上的所有内容。如果您对我们的文档有任何反馈，请发送 git pull 请求或发表在 [docs GitHub repo][4] 上！

In this article I want to teach you how to make a basic Decentraland scene **interactive**. I want to keep it very simple. We're not going to create a fully-fledged game, just something that responds to user interaction in basic ways.

在这篇文章中，我想教你如何来制作一个基本的 Decentraland **互动**场景。我会尽量简单地阐述。我们不打算创建一个完全成熟的游戏，只是用一些基本方式来响应用户交互。

As you read along, you can check out the [source code][5] for the scene, or follow along and create your own scene from scratch. While all of the concepts I'll cover apply to games, I want to showcase them in a less technically ambitious scene. I'll leave that for future posts.

在您阅读时，您可以查看场景的[源代码][5]，或者从头开始创建自己的场景。虽然我要介绍的所有概念都适用于游戏，但我希望在不那么技术的场景中展示它们。技术复杂的我将留待以后发表。

For today's post, we'll build something closer to interactive art than to a game; picture a virtual equivalent of the kind of installation you find in modern, trendy museums accompanied by confusing descriptions with the words "embodied" and "human condition".

今天，我们将创建一个更象是互动艺术而不是游戏的东西；想象一个你在现代的、时髦的博物馆里找到的，带有让人困惑的“象征”和“ human condition 人类的处境”之类描述的一个装置的虚拟等价物。

To deal with interactive scenes, there are two key concepts that we need to cover: **events** and the scene's **state**.

为了处理交互式场景，我们需要涵盖两个关键概念：**event** 和场景的 **state**。

**Events** represent things that happen. They are typically things that the user does, like click on an entity or walk around the scene.

**Events** 代表发生的事情。它们通常是用户所做的事情，例如点击实体或在场景中走动。

The scene **state** is the current condition of the scene at any given time, represented as a set of variables that may change over time, usually in response to events.

场景的 **state** 是任何给定时间时场景的当前状态，表示为一组可能随时间变化的变量，通常是对事件的响应。

### Build your scene

### 构建你的场景

If you're building your own scene as you read, you should already have [created your first scene][6], and have the default [Hello World scene][7] already built up.

如果阅读时您正在构建自己的场景，那么确保您已经[创建了你的第一个场景][6]，并已有了默认的 [Hello World 场景][7]。

If you open the scene.tsx file, you'll note that it contains a basic sample scene. Delete everything in it so that you're left with the bare essentials:

如果打开 scene.tsx 文件，您会注意到它包含一个基本的示例场景。删除中括号中的所有内容：

### Respond to clicks

### 响应点击事件

Let's start out with an easy use case: the user clicks somewhere, creating an event. The event triggers a function that changes the scene state, and the new scene state causes the scene to be rendered with visible differences.

让我们从一个简单的用例开始：用户点击某处，创建了一个事件。该事件触发一个改变场景状态的函数，新的场景状态使得场景跟先前的场景明显不同。

I'm still not sure what I want to do with my sample scene, but I know I want to do something _artistic_. So, let's start by building a pedestal to display some sort of virtual sculpture.

我仍然不确定我想对我的示例场景做什么，但我知道我想做得有艺术些。所以，让我们从构建一个底座来展示某种虚拟雕塑开始吧。

We want to make our art exhibit interactive, so let's have the pedestal change color when the user clicks on it.

我们希望让我们的艺术展览具有互动性，所以当用户点击它时，我们让底座改变颜色。

First, we need to take care of three things:

首先，我们需要处理三件事：

* **Define a scene state** that includes a variable that represents the pedestal's color and keeps track of its changes.

* **定义一个场景状态**，其中包含一个表示底座颜色的变量并跟踪其变化。

* **Place a pedestal entity in the scene**, and set its color to reference the variable in the scene state.

* **在场景中放置一个底座**，并设置其颜色为场景状态中的变量。

* **Change the variable's value** in the scene state every time that the user clicks on the pedestal, randomly choosing from a list some predefined colors.

* 每次用户点击底座时，在场景状态下**更改变量的值**，从预定义的颜色列表中随机选择。

We'll now define a scene state. So far, the only thing we need to keep track of in the scene is the color of the pedestal, so we'll declare that as our only variable, giving it an initial color of grey (expressed as a hexadecimal value).

我们现在定义一个场景状态。到目前为止，我们在场景中唯一需要跟踪的是底座的颜色，因此我们将其声明为唯一的变量，给它一个灰色的初始颜色（表示为十六进制值）。

Nice going! So far, this variable still doesn't manifest itself in our scene in any visible way. We'll create our pedestal as a simple cylinder entity, and we'll set the pedestal's color to reference the `pedestalColor` variable we created in the scene's state.

不错！到目前为止，这个变量仍然没有以任何可见的方式在我们的场景中表现出来。我们将创建一个简单的圆柱实体作为底座，设置底座的颜色为我们在场景状态中创建的 `pedestalColor` 变量。

We'll define an array of color values that we can randomly choose from in the .tsx file, but this will sit outside the definition of our custom scene class, that way it can be referenced from anywhere in the file.

我们来定义一个颜色值数组，这样我们可以从 .tsx 文件中随机选择，我把它定义在我们的自定义场景类之外，这样就可以从文件中的任何位置引用它。

Using this array, we can choose a color by referring to a position in the array, which will be very handy later on when we pick colors by generating a random number.

使用这个数组，我们可以通过引用数组中的位置来选择颜色，这样稍后当我们通过生成随机数来选择颜色时会非常方便。

The final thing our sample needs is a way for the value of `pedestalColor` to change, otherwise the scene isn't really interactive, is it? To do that, we initiate an `eventSubscriber` so that it carries out an asynchronous function whenever an event of type `pedestal_click` occurs.

我们的示例最后一件事是要改变 `pedestalColor` 的值，否则场景就不是真正交互式的，是吧？为此，我们设计一个 `eventSubscriber`，以便在发生类型为 'pedestal_click` 的事件时执行异步函数。

Since we want this `eventSubscriber` to start listening for click events as soon as our scene is loaded, we initiate it as part of the `sceneDidMount` function; this function is called only once, when the scene is ready to be shown to the user.

因为我们希望这个 `eventSubscriber` 在加载场景后立即开始侦听点击事件，所以我们将它作为 `sceneDidMount` 函数的一部分启动；仅当场景准备好向用户显示时，此函数被调用，并且只调用一次。

Since the id of the clicked entity is `pedestal`, the click event is named `pedestal_click`. We don't need to define this event name anywhere, the SDK generates it automatically based on the entity id.

由于被点击的实体的 id 是 `pedestal`，因此 click 事件被命名为 `pedestal_click`。我们不需要在任何地方定义此事件名称，SDK 会根据实体 ID 自动生成。

![][10]

Now is a good time to run a preview of your scene.

现在是时候运行场景预览了。

Start your preview by running `dcl preview` in your terminal or command prompt. Every time you click on the pedestal, the `pedestalColor` variable changes. Each time something changes in the scene state, the scene is rendered again using the new values of the scene state.

在终端或命令提示符下运行 `dcl preview` 开始预览。每次单击底座时，`pedestalColor` 变量就会发生变化。每次场景状态发生变化时，都会使用场景状态的新值再次渲染场景。

We added a `console.log(myColors[col])` statement to the function that changes the pedestal's color. Logging messages is a good way to gain insight into your code in case it doesn't behave as expected. This is especially handy when you're dealing with things that are invisible, like the scene state or events.

我们在改变底座的颜色的函数中添加了一个 `console.log（myColors [col]）` 语句。在程序行为不符合预期时，通过日志记录是深入了解代码的好方法。特别是当您处理不可见的事物（如场景状态或事件）时，尤为方便。

To view the logged messages while running a preview of your scene, you need to look at your browser's JavaScript console, which you can open in the developer settings of your browser. You should see the hexadecimal values of the colors printed out as they change.

要在运行场景预览时查看日志记录的消息，您需要查看浏览器的 JavaScript 控制台，您可以在浏览器的开发人员设置中打开它。在此您应该能看到颜色的十六进制值在更改时被打印出来。

### Optional: build a fancier pedestal

### 可选：构建一个更高级的底座

The SDK lets us add several types of entities with basic shapes, what are commonly called _primitives_, but we can also define our own custom entity types. If we want our pedestal to be made up of a combination of several shapes but still behave as a single entity, we can define a custom "pedestal" type and add that instead.

SDK 允许我们添加多个基本形状的实体，通常称为_基本形体_，但我们也可以定义自己的自定义实体类型。如果想让我们的底座由多个形状组合而成，但其表现仍然为单个实体，我们可以加入一个自定义的 “pedestal” 类型来代替。

To do this, create a new file called pedestal.tsx, preferably in a folder named `/src` in your scene. Then, add the following code, which defines a pedestal as two box entities in relative positions to a base entity. The code also defines an _interface_ for our new type, this determines what parameters can be passed to the entity to customize it.

为此，新创建一个名为 pedestal.tsx 的新文件，最好放在场景中名为 `/ src` 的文件夹中。然后，添加以下代码，这些代码将底座定义为由两个相对位置的长方形盒子组成的一个实体。并且为我们的新类型定义了_接口_，来决定哪些参数可以传递给实体，从而实现对实体的自定义。

We need to add an invisible `<entity>` to wrap our two box entities, this is because type definitions need to generate a single root entity. We can't have two loose box entities at root level, they have to be children of a single parent.

我们需要添加一个不可见的 `<entity>` 来包装我们的两个实体，这是因为类型定义需要生成一个根实体。我们不能在根级别拥有两个盒子实体，它们必须是一个父级的子级。

Also note that the way in which we set the color of the entities has changed. This is because we're no longer writing in the _scene.tsx _file, so we can't refer to the scene state directly. The expression `this.state.pedestalColor` is no longer valid because the word `this` no longer refers to the scene object, it refers to the instance of the pedestal entity.

另请注意，我们设置实体颜色的方式已更改。这是因为我们的代码不在 _scene.tsx_ 文件中，所以我们不能直接引用场景状态。表达式 `this.state.pedestalColor` 不再有效，因为 `this` 不再引用场景对象，这里指的是底座实体的实例。

To access information from `pedestalColor` in the scene state, we need to pass its value to a `color` property that belongs to the instance of the pedestal entity, then we use it to set the color of the boxes through the expression `props.color`. This might make more sense when you see how we add the pedestal entity to the scene.

要在场景状态下从 `pedestalColor` 访问信息，我们需要将其值传递给底座实体实例的 `color` 属性，然后我们通过表达式 `props.color` 来设置盒子的颜色。当看到我们如何将底座实体添加到场景时，你就明白了。

Back in our main _scene.tsx_ file, we need to import the Pedestal type from the file we just created, otherwise our scene won't even know that it exists.

回到我们 _scene.tsx_ 这个主要的文件中，我们需要从刚创建的文件中导入 Pedestal 类型，否则我们的场景甚至不知道它的存在。

Instead of adding a cylinder as we did before, we now add an object of type Pedestal, and set values for the properties we defined in its interface.

不同于添加一个柱面，现在我们添加一个 Pedestal 类型的对象，并设置我们在接口中定义的属性的值。

Note that you can only set parameters that you defined in the interface of your custom type, in this case: _id_, _position,_ and _color_. If we want to make our pedestal type more adaptable, we could add more properties to the interface like rotation and scale. Also note that we're passing the value of `this.state.pedestalColor` to the entity's property `color`. This value is updated each time the scene state changes.

请注意，您只能设置在自定义类型的界面中定义的参数，在这里是：_id_，_position_ 和 _color_。如果我们想让我们的底座类型更具适应性，我们可以为接口添加更多属性，如旋转和缩放。另请注意，我们将 `this.state.pedestalColor` 的值传递给实体属性 `color`。这个值在每次场景状态更改时都会更新。

![][12]

### Add looping animations

### 添加循环动画

Now it's time to put something on that pedestal and have it slowly spin in circles so that we can better admire it. Google Poly is full of free models you can use. Many are available as _.glTF_ files that you can import directly into a Decentraland scene. I found this [adorable work of art][13] and instantly fell in love with how …special it is (thanks Will Thompson for uploading it with a free licence!).

现在是时候把东西放在底座上，并让它慢慢旋转，这样我们就可以更好地欣赏它了。 Google Poly 有很多您可以免费使用的模型。其中大部分提供了可以直接导入 Decentraland 场景的 _.glTF_ 格式文件下载。我找到了这个 [adorable work of art][13]，并立刻喜欢上了......它很特别（感谢 Will Thompson 的上传并提供免费许可！）。

![][15]

Most low-poly meshes that you download from Google Poly can be uploaded directly into a Decentraland scene, but with this one I ran into a problem: it had an extremely large number of vertices (over 12,000). Most of these vertices were not even visible, as it was all made from many overlapping spheres.

大多数从 Google Poly 下载的低多边形场景文件可以直接上传到 Decentraland 场景中，但是在这个场景中我遇到了一个问题：它使用了极大数量的顶点（超过 12,000 个）。大多数这些顶点甚至都不可见，因为它全部由许多重叠的球体组成。

Since I really really wanted to use this model, I imported it into Blender and simplified its structure, without compromising its beauty. I used the _BoolTool_ Blender add-on to remove all the internal faces of the model, then I used the _decimate modifier_ to simplify its geometry. Finally, I exported the model back to a glTF file.

因为我真的是很想使用这个模型，所以我将它导入 Blender，在又不影响它的美观的同时简化了它的结构。我使用 _BoolTool_ Blender 附加组件删除了模型的所有内部面，然后使用 _decimate modifier_ 简化其几何体。最后，我将模型用 glTF 文件导出。

The code for getting this model to rotate in your scene is similar to what we used for clicking the pedestal:

在场景中，让此模型旋转的代码与我们单击底座的代码类似：

* Add a new variable to the scene's state that represents the dog's current rotation.

* 在场景的状态中添加一个新变量，表示当前狗的旋转。

* Place an entity in the scene for the dog model and set its rotation to reference that variable you just created.

* 将狗模型的实体放置在场景中，并将其 rotation 设置为刚刚创建的变量。
  
* Change the value of the variable at a regular interval.

* 定期更改变量的值。

Here's the new scene state, including the variable that represents the dog's rotation.

这是新的场景状态，包括狗旋转的变量。

In the `sceneDidMount` function, the same place where we initiated the click event listener, we can initiate the rotation of the dog. We do this by adding a `setInterval` statement, this performs a function regularly at a given interval.

在 `sceneDidMount` 函数中，在我们启动 click 事件监听器的同一个地方，我们来初始化狗的旋转状态。我们通过添加 `setInterval` 语句来执行此操作，它将以给定的时间间隔定期执行函数。


This function changes the dogAngle variable in the scene state every 100 milliseconds. It doesn't matter if the value of `dogAngle` ends up rising well above 360, its values will keep being interpreted as a rotation.

此函数每 100 毫秒更改场景状态中的 dogAngle 变量。 `dogAngle` 值最终上升到 360 以上是没有关系的，它的值将被继续解释为旋转。

Finally, we'll add our precious dog to the `render()` function, positioned on top of the pedestal:

最后，我们将把我们珍贵的狗加入 `render（）` 函数，放置在底座顶部：


Note that the _y_ axis of the rotation references the new variable we added to the scene state, we don't care about rotating it along the _x_ or_ z_ axis so those values are set to 0.

请注意， _y_ 轴旋转引用了我们添加到场景状态的新变量，我们不关心沿 _x_ 或 _z_ 轴的旋转，因此这些值设置为 0。

We also added a _rotation_ _transition_ to the entity, transitions make changes occur smoothly. If you comment out the line in the code where we add the transition, you'll notice that the rotation works, but it looks jumpy. That's because we're updating the scene state at a rate which is different from the frames per second at which the scene is being rendered. A transition guarantees that the dog will rotate smoothly. Notice that the duration we set for the transition (100 milliseconds) matches the interval at which the rotation is being updated.

我们还向实体添加了 _rotation_ _transition_ ，transitions 能使更改平滑。如果注释掉我们添加 transitions 的代码的那一行，你会注意到其能够旋转，但看起来很神经质。那是因为我们正在以与每秒渲染场景的帧数不同的速率更新场景状态。transition 可确保狗平滑地旋转。请注意，我们的 transition 设置的持续时间（100毫秒）与更新轮换的时间间隔相匹配。

So there you have it, our dog is now turning smoothly for you to admire. I also added some details to the scene so that it looks a little more like a museum worthy of exhibiting this.

搞定，我们的狗正在平滑的旋转，供你欣赏。我还在场景中添加了一些细节，使它看起来更像是一个用来展示的博物馆。

![][17]

### Track and respond to the user's position

### 跟踪用户的位置并作出响应

Clicks aren't the only events that the user generates while navigating your scene. Every time the user moves or even turns to look around, a new event is generated. The `positionChanged` event contains all of the relevant information that is generated with it: the id of the user that moved and the coordinates of its new location. We can use this information to alter the scene state however we want.

点击并不是用户在导航场景时生成的唯一事件。每次用户移动或甚至转身环顾四周时，都会生成一个新事件。 `positionChanged` 事件包含生成此事件的所有相关信息：正在移动的用户的 id 和新位置的坐标。我们可以使用这些信息来改变我们想要的场景状态。

Our scene is missing something a bit more outrageous, so we'll now add an object that rotates based on the user's position. I like how this interaction works, because it catches you off guard when you realize that your walking is causing the rotation, and that the direction of the rotation depends on the direction in which you walk.

我们的场景遗漏了一些东西，所以我们现在添加一个根据用户位置旋转的对象。我喜欢这种交互工作，因为当你意识到是你的行走引起了它的旋转时，你会为此感到惊奇，并且旋转的方向取决于你行走的方向。

Using Blender, I created a 3D model of a giant flying donut spiral. Why? It's art, it can mean a lot of things to different people, and it's easier to make you do the thinking.

在 Blender 中，我创建了一个大型的螺旋状飞行甜甜圈 3D 模型。为什么用这个模型？这是艺术，对不同的人，它可能意味着很多事情，并且更容易引你思考。

The model was fairly easy to create, I just added a _torus_ mesh (which is naturally shaped like a donut) and used the _array modifier_ to multiply it into a bunch of cloned shapes. I then exported them all as a single _glTF_ file. If you want to use the donut spiral model for your projects, you can copy it from the scene repo.

该模型相当容易创建，我只是添加了一个圆环面（自然形状像甜甜圈）并使用 _array modifier_ 将它克隆成一大堆。然后我将它们全部导出为单个 _glTF_ 文件。如果你想在你的项目中使用圆环螺旋模型，可以从场景仓库中复制。

The steps to add this to our scene should start to feel familiar:

将此添加到我们的场景的步骤，应该开始让你感到熟悉了吧：

* Add a new variable to the scene state to represent the spiral's current rotation:

* 将新变量添加到场景状态，用以表示螺旋的当前旋转：

* Add a `gltf-model` entity and set its rotation to match our newly created variable:

* 添加一个 `gltf-model` 实体并设置 rotation 为我们新创建的变量：

<gltf-model src="models/donutnado.gltf" scale="{0.8}" position="{{x:5," y:8.5,="" z:5}}="" rotation="{{y:this.state.donutAngle," x:0,="" z:0}}="" transition="{{" rotation:="" {="" duration:="" 100,="" timing:="" "linear"="" }="" }}="">

<gltf-model src =“models / donutnado.gltf”scale =“{0.8}”position =“{{x：5，”y：8.5，=“”z：5}} =“”rotation =“{{ y：this.state.donutAngle，“x：0，=”“z：0}} =”“transition =”{{“rotation：=”“{=”“duration：=”“100，=”“timing ：=“”“linear”=“”} =“”}} =“”>

Note that we also set a transition on the rotation, this will make it rotate smoothly.

请注意，我们还在旋转上设置了一个 transition ，这有助于平滑旋转。

* Add a `subscribeTo` method that runs an asynchronous function each time a `positionChanged` event occurs. Initiate this in the `sceneDidMount` function as we did before, in this way it will start monitoring the user's position as soon as the scene is loaded.

* 添加 `subscribeTo` 方法，每次发生 `positionChanged` 事件时运行异步函数。像我们之前一样在 `sceneDidMount` 函数中进行初始化，这样一旦场景加载，它就会开始监视用户的位置。


The `subscribeTo` method is similar to the `eventSubscriber` method we used for clicking the pedestal, but by using `subscribeTo` you can also access information that arrives with the event object. Here we're setting the `donutAngle` variable to an addition of the _x_ and _z_ coordinates of the user's position.

`subscribeTo` 方法类似于我们用于单击底座的 `eventSubscriber` 方法，但是通过使用 `subscribeTo`，您还可以访问跟事件对象一起的信息。这里我们将 `donutAngle` 变量设置为添加用户位置的 _x_ 和 _z_ 坐标。

![][19]

When moving to the right or forward, the donuts turn left, when moving to the left or backwards, the donuts turn right, and when staying still, the donuts stay still as well. This is all very disconcerting, I love it.

当向右或向前移动时，甜甜圈向左转，当向左或向后移动时，甜甜圈向右转，当保持静止时，甜甜圈保持静止。这会让人感到惊讶，我喜欢它。

There's a downside to how our spiral behaves: if you move diagonally, the X coordinate rises while the Z coordinate drops causing both coordinates add up to zero which keeps the donuts still. There are ways you could change the code to prevent that from happening, but to keep things simple, let's assume that we're ok with how it works.

我们的螺旋行为有一个缺点：如果你沿对角线方向移动，X 坐标会上升，而 Z 坐标会下降，导致两个坐标加起来为零，这使得甜甜圈保持不变。有一些方法可以改变代码以防止这种情况发生，但为了简单起见，让我们假设这样没有问题。

### SDK Best Practices: tip of the day

### SDK 最佳实践：每日提示

Your scene state can contain as many different variables as you want, but the state object containing these variables can be defined as a type of its own. This ensures that the state object always has the right variables and that they all have valid values for their corresponding types.

您的场景状态可以包含任意数量的不同变量，且可以把包含这些变量的状态对象定义为它自己的类型。这可以确保状态对象始终具有正确的变量且它们都具有相应类型的有效值。

First, create a state interface, then pass the type of this interface as the second property of your custom scene class, which sets the type for the state object. If you're working with an advanced code editor like _Visual Studio Code_ or _Atom_, defining a state interface helps your editor provide type validation and smart auto-completes, which can save you from a lot of headaches.

首先，创建一个状态接口，然后将此接口的类型作为传递给自定义场景类的第二个属性，以此设置状态对象的类型。如果您正在使用高级代码编辑器（如 _Visual Studio Code_ 或 _Atom_），则定义状态接口可帮助您的编辑器提供类型验证和智能自动完成，这可以帮您减少许多麻烦。


### Final thoughts

### 最后的想法

Interactive art is often not about the aesthetic value of the thing you're seeing itself, but rather about the _mapping_ between your actions and how the piece responds, and how that makes you feel. As for this piece, it probably just makes you feel dizzy. Nevertheless, do consider that there are clever ways in which the mapping between a user's actions and the changes in the scene's state can be used to make you feel, for example, empowered or powerless in different ways, and imagine how that can be used to convey artistic meaning.

互动艺术往往无关于你所看到的东西的审美价值，而是关于你的行为与作品之间反应的_映射_，以及给你的感受。至于这件作品，它可能只会让你感到头晕。然而，请思考一下，一定存在一些聪明的方法，使得用户的动作和场景状态的变化之间的映射，能让你有所感受，例如，各种方式的掌握或无力，并想象如何用它来表达艺术含义。

So that's all for today. I hope this tutorial inspires you to create more interactive scenes. Whether you're aspiring to create some kind of interactive art, a game, or just something you think looks and feels nice, what you do with the SDK is totally up to you!

今天的教程就此结束。我希望本教程能够激发您创建更多的交互式场景。无论您是想要创建某种互动艺术、游戏、还是你认为看起来和感觉美好的东西，使用 SDK 能做什么完全取决于您！

### Join the conversation

### 加入对话

* [Discord][20]

* [Twitter][21]

* [Reddit][22]

* [Telegram][23]

* [Get started with the SDK!][24]

* [开始使用SDK！] [24]

[1]: https://cdn-images-1.medium.com/freeze/max/60/1*0r-9jJtFak1GgM2vrg8LVw.png?q=20
[2]: https://cdn-images-1.medium.com/max/2000/1*0r-9jJtFak1GgM2vrg8LVw.png
[3]: https://docs.decentraland.org/
[4]: https://github.com/decentraland/documentation
[5]: https://github.com/decentraland/sample-scene-simple-interactive
[6]: https://docs.decentraland.org/documentation/create-scene/
[7]: https://github.com/decentraland/sample-scene-static
[8]: https://cdn-images-1.medium.com/freeze/max/60/0*r5HPG-R3k8SYrBo4?q=20
[9]: https://blog.decentraland.org/undefined
[10]: https://cdn-images-1.medium.com/max/1600/0*r5HPG-R3k8SYrBo4
[11]: https://cdn-images-1.medium.com/freeze/max/60/0*5faBdYE2oWWlcOV_?q=20
[12]: https://cdn-images-1.medium.com/max/1600/0*5faBdYE2oWWlcOV_
[13]: https://poly.google.com/view/7wJHHY5Sjq7
[14]: https://cdn-images-1.medium.com/freeze/max/60/0*gv_h-0ClBr1nJrP0?q=20
[15]: https://cdn-images-1.medium.com/max/1600/0*gv_h-0ClBr1nJrP0
[16]: https://cdn-images-1.medium.com/freeze/max/60/0*zmVDf3AEw0iBnkjN?q=20
[17]: https://cdn-images-1.medium.com/max/1600/0*zmVDf3AEw0iBnkjN
[18]: https://cdn-images-1.medium.com/freeze/max/60/0*UtutrdqDKA21yZDa?q=20
[19]: https://cdn-images-1.medium.com/max/1600/0*UtutrdqDKA21yZDa
[20]: https://discordapp.com/invite/9EcuFgC
[21]: https://twitter.com/decentraland
[22]: https://www.reddit.com/r/decentraland/
[23]: https://t.me/decentralandTG
[24]: https://developers.decentraland.org/
