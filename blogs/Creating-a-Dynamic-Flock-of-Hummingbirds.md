
# Developer Tutorial: Creating a Dynamic Flock of Hummingbirds

# 开发者教程：创建动态蜂鸟群

## Learn how to animate 3D models and spawn multiple entities in your Decentraland scenes

## 了解如何在 Decentraland 场景中为 3D 模型制作动画并生成多个实体

![][2]

In this article, we'll build a scene that animates a swarm of hummingbirds that fly randomly around the scene. I chose hummingbirds not just because they're adorable, but also out of convenience: they can fly in place and maneuver very agilely. This makes it easier to program their behavior, as you'll see later.

在本文中，我们将构建一个一群蜂鸟在场景中随机飞行的场景。我选择蜂鸟的原因不仅是因为它们长得可爱，还因为开发便利：它们可以原地飞行并且移动灵活。如同您在后面看到的一样，对其行为进行编程可以更轻松。

My name is Nicolas Earnshaw, and I take care of the Decentraland documentation. That means everything you can find in [docs.decentraland.org][3]. If you have any feedback on our docs, please make a pull request or create an issue on the docs [GitHub repo][4]!

我是 Nicolas Earnshaw，负责 Decentraland 的文档。意即[docs.decentraland.org][3] 上的所有内容。如果您对我们的文档有任何反馈意见，请提交请求或在 [GitHub repo][4] 上创建问题！

[In my previous article on building interactive scenes][5], we went over some fundamentals of using the SDK, including how scene states and events are handled. In this article I want to go a little bit deeper and tackle two very important concepts that I personally found quite mysterious when I first started to use the Decentraland SDK. We'll create a sample scene that doesn't just look pretty but also showcases:

[在我之前关于构建交互式场景的文章][5]中，我们讨论了使用 SDK 的一些基础知识，包括如何处理场景状态和事件。在本文中，我想更深入地解决两个非常重要的概念，当我第一次开始使用 Decentraland SDK 时，我个人觉得这些概念非常神秘。我们将创建一个示例场景，它不仅看起来漂亮而且还展示了：

1. How to animate a 3D model

1. 如何为 3D 模型制作动画

2. How to handle an undetermined amount of entities

2. 如何处理未确定数量的实体

A lot of how the SDK works is heavily inspired by [React.js][6]. If you're already a React master, handling multiple entities will probably come easily to you. If not, don't worry, you don't need any familiarity with React in order to follow along with this tutorial.

SDK 的很多工作方式受到 [React.js][6] 的启发。如果您已经熟悉 React，那么处理多个实体可能对您很容易。如果不是，也请不要担心，您不需要熟悉 React 就可以按照本教程进行操作。

![][8]

This is how our scene will look when we're done.

这就是完成后的场景。

You can find the code and models for this tutorial in [this repo][9]. Or, you can build your own scene as you follow along. If you ever get stuck along the way or want to skip ahead to another section, you can download the code for the scene at one of its intermediate stages by clicking on the releases tab and selecting one of the releases. Each release matches up with one of the sections of this document.

您可以在[这个 github 库][9]中找到本教程的代码和模型。或者，您可以随意构建自己的场景。如果中间遇到问题困住或想要跳到另一个节，您可以通过单击版本选项卡并选择其中一个版本，下载各阶段的场景代码。每个版本都对应本文档的一个部分。

### Find and animate a 3D&nbsp;model

### 查找并制作 3D 模型的动画

I found this very nice [3D model of a hummingbird][10] that we'll use from Poly by Google, licensed under [CC BY][11]. The model has no animations of its own, so we will have to animate it ourselves. For that, we must download it as an&nbsp;_.obj_ file, and import it into [Blender][12].

我在 Google Poly 发现这个非常好看的[蜂鸟 3D 模型][10]，由[CC BY][11]许可下载使用。该模型没有自己的动画，因此我们必须自己制作动画。为此，我们选择 _.obj_ 文件下载，并将其导入[Blender][12]。

The first thing you need to do is build an armature to represent the different movable parts of the model. Keep it simple, you don't need to represent the bird's entire skeleton, just the parts that you intend to move.

您需要做的第一件事是构建一个 armature 骨骼支架来表示模型不同的可移动部分。为了简单，你不需要表现鸟的整个骨架，只需要你想要移动的部分。

![][14]

Then you need to link the armature to the model by making the armature a child element of the bird mesh. Once matched, move the parts of the armature around to check that the mesh follows it in ways that look natural. If the model gets deformed in weird ways, then you can use weight paint to change what parts of the model are affected by each bone in the armature.

然后，您需要将骨骼支架连接到模型，方法是将骨骼支架设置为峰鸟网格的子元素。匹配后，移动骨骼支架周围的部分以检查网格是否以看起来自然的方式跟随。如果模型以奇怪的方式变形，那么您可以使用 weight paint 来更改模型的哪些部分受到骨骼支架中骨骼的影响。

Next, you need to set the armature into a series of poses over time to create the actual animations. The transition between each pose occurs smoothly by default. If the animation will be looped in your scene, make sure the final pose is identical to the starting pose to avoid jumpiness.

接下来，随着时间变化，你需要将骨骼支架设置成一系列的姿势来创建实际的动画。默认情况下，每个姿势之间是平滑过渡的。如果动画将在场景中循环，请确保最终姿势与起始姿势相同，以避免跳动。

![][16]

To create several animations, select the _Dope-Sheet_ view, and open the _Action Editor_. You can also use the _Dope-Sheet_ view to edit the frames, like adjusting the time between two frames or making a frame store only the position of certain bones of the armature.

要创建多个动画，请选择 _Dope-Sheet_ 视图，然后打开 _Action Editor_。您还可以使用_Dope-Sheet_ 视图来编辑帧，例如调整两帧之间的时间或使帧仅存储骨架支架的某些骨骼的位置。

I created three animations with this model: _fly_, _look,_ and _shake_. Note that _fly_ only moves the bird's wings whilst _look_ and _shake_ only move the bird's head.

我用这个模型创建了三个动画：_fly_，_look，_和_shake_。请注意，_fly_仅移动鸟的翅膀，而_look_ 和 _shake_ 仅移动鸟的头部。

To export a model from Blender in _glTF_ format, you need to first install an add-on. There are several out there, but we have found that some have issues with animations. In our experience, this add-on by [Kupomar][17] works best.

要以 _glTF_ 格式从 Blender 导出模型，您需要先安装插件。有几个这样的插件，但我们发现有些插件在动画方面有问题。根据我们的经验，[Kupomar][17] 这个插件效果最好。

### Add a single bird and animate&nbsp;it

### 添加一只鸟并制作动画

Create a new Decentraland scene by following the steps in [create your first scene][18]. For the scene type, be sure to select _Interactive_, the second option.

按照[创建你的第一个场景][18]中的步骤创建一个新的 Decentraland 场景。对于场景类型，请务必选择第二个选项 _Interactive_。

Once the scene is created, create a new _models_ folder inside the scene folder and add the _glTF_ file you exported from Blender.

创建场景后，在场景文件夹中创建一个新的 _models_ 文件夹，放入从 Blender 导出的 _glTF_ 文件。

Now open the scene's _scene.tsx_ file and delete what's in the `render()` function to replace it with this:

现在打开场景的 _scene.tsx_ 文件并删除 `render()` 函数中的内容，将其替换为：

```typescript
async render() {
  return (
    <scene>
      <gltf-model
        src="models/hummingbird.gltf"
        position={{x:5, y:1, z:5}}
        skeletalAnimation={[
            { clip: "Bird_fly" , playing: true, loop:true },
            { clip: "Bird_shake" , playing: true, loop:true }
        ]}
      />
    </scene>
  )
}
```


The _gltf-model_ entity we're adding here uses two of the animations we created in Blender: _Bird_fly_ and _Bird_shake_. If you're not sure how the animations are named in the _glTF_ file, you can easily check them by opening the file. We can run two animations at the same time because they don't overlap: _Bird_fly_ only contains information about wing positions and _Bird_shake_ only contains information about head positions. If your animations do overlap, you can always use the _weight_ property to calculate a weighted average of what each animation tells it to do.

我们在这里添加的 _gltf-model_ 实体使用了我们在 Blender 中创建的两个动画：_Bird_fly_ 和  _Bird_shake_。如果您不确定在 _glTF_ 文件中动画的名称，可以打开文件内容查看。我们可以同时运行两个动画，因为它们不重叠：_Bird_fly_ 仅包含有关翅膀位置的信息，_Bird_shake_ 仅包含有关头部位置的信息。如果您的动画确实重叠，您可以使用 _weight_ 属性来设置计算每个动画的加权平均值。

This is a good time to check our scene to make sure our little friend is looking and behaving as we expected.

现在检查我们的场景，确保我们的“小朋友”行为符合我们的预期。

![][20]

WHAT IS THAT THING, IT'S TERRIFYING! At least it works and is moving just as we expected, but it's unnaturally huge. Let's resize our model for Decentraland.

这是什么，好吓人！不过至少可以工作了，并且正如我们预期的那样移动，但是它太大了点。让我们调整下 Decentraland 模型。

### Change the hummingbird's position over&nbsp;time

### 随时间改变蜂鸟的位置

Besides shrinking the hummingbird's size, we want it to fly randomly around the scene. To do this, we need to represent its position as a variable in the scene state, update this variable regularly, and then reference the value of this variable whenever we render the scene.

除了缩小蜂鸟的大小外，我们希望它能在场景中随机飞行。为此，我们需要在场景状态中将其位置表示为变量，定期更新此变量，然后在渲染场景时引用此变量的值。

We will first create a new scene state and add our own `birdPos` variable.

我们将首先创建一个新的场景状态并添加我们自己的 `birdPos` 变量。


```typescript
state: IState = {
  birdPos: {x:5, y:1, z:5},
}

```

Also change the contents of the `IState` interface to reflect this.

还要更改 `IState` 接口的内容来反映这一点。


```typescript
export interface IState {
  birdPos: Vector3Component,
}
```

Note that our code editor underlines _Vector3Component_ in red, that's because we must first import this class to our file.

请注意，我们的代码编辑器在 _Vector3Component_ 上使用了红色下划线，这是因为我们必须先将此类导入到我们的文件中。

```typescript
import {Vector3Component} from 'metaverse-api'
```

Then we need to initiate a time-based loop in `sceneDidMount()` function, calling a simple function that creates a random coordinate and sets it as the new value of `birdPos`.

然后我们需要在 `sceneDidMount（）` 函数中启动一个基于时间的循环，调用一个创建随机坐标的简单函数并将其设置为 `birdPos` 的新值。

```typescript
sceneDidMount() {
  setInterval(() => {
    this.newBirdPos()
  }, 4000)
}
newBirdPos() {
  const newPos = {
    x: (Math.random() *10 ),
    y:  Math.random() *2 + 1,
    z: (Math.random() *10 )
  }
  this.setState({birdPos: newPos})
}

```

The final step is to make the position of the bird take its value from `birdPos`.

最后一步是让鸟的位置从 `birdPos` 中获取其值。

Let's also please, please make it smaller so I don't jump out of my chair again when we preview the scene!

还有，请把它变小，让我在预览场景时不会再次从椅子上跳起！

```typescript
async render() {
  return (
    <scene >
    <gltf-model
      src="models/hummingbird.gltf"
      scale={0.2}
      position={this.state.birdPos}
      transition={{
        position: { duration: 500, timing: "ease-in-out" }
      }}
      lookAt={this.state.birdPos}
      skeletalAnimation={[
        { clip: "Bird_fly" , playing: true, loop:true },
        { clip: "Bird_shake" , playing: true, loop:true }
      ]}
    />
  </scene>
  )
}
```

We added four new things to the `gltf-model` entity:

我们在 `gltf-model` 实体中添加了四个新东西：

* `scale` is now 0.2. this makes the bird smaller. _Thank goodness_.

* `scale` 现在设为 0.2。这使鸟变小了。 _谢天谢地_。

* `position` references `birdPos` instead of a fixed value. Each time this variable changes, the `render()` function is called again to produce a new output.

* `position` 引用 `birdPos` 而不是固定值。每次这个变量改变时，就会调用 `render()` 函数来产生一个新的输出。

* `transition` handles changes in the bird's position. Without it, we would just see it teleport from one position to the next. We set `timing` to _ease-in-out_, which I think looks quite natural as the bird builds up speed and then slows down gradually. Note that the duration of the transition is fixed at 500 ms, this means that it will vary its speed depending how far the next random point is. I first thought of this as a temporary solution, but I liked how it looked. Let's keep it like that.

* `transition` 处理鸟的位置变化。没有它，我们只会看到它从一个位置突然到另一个位置。我们将 `timing` 设置为 _ease-in-out_，这样看起来非常自然，因为鸟会加快速度，然后逐渐减慢速度。请注意，转换的持续时间固定设为 500 毫秒，这意味着它将根据下一个随机点的距离来改变其速度。我原来只把它当成一个临时解决方案，但我觉得不错。那就这样吧。

* `lookAt` makes the bird always turn to face a specific point in space, in this case its next position. When using `lookAt`, you don't need to think of rotation in terms of angles, the SDK calculates them for you. Although it's a known fact that hummingbirds are remarkably good fliers and are capable of flying backwards and sideways, it would look kind of silly if they kept their orientation fixed as they flew around.

*`lookAt` 使鸟总是转向面对空间中的特定点，这里转向它的下一个位置。当使用 `lookAt` 时，您不需要考虑旋转角度，SDK 会为帮你您计算。虽然众所周知，蜂鸟是非常好的飞行员并且能够向后和向侧面飞行，如果它们在飞行时保持其方向固定，那将会显得有些愚蠢。

Here's how the scene looks now:

这是现在场景的样子：

![][22]

This works quite well. A lot less scary. And I don't know about you, but I feel that the way it moves around the scene is quite convincing.

这非常有效。不那么吓人了。我不知道你们怎么看，但我觉得它在场景中移动的方式很有说服力。

### Switch animations randomly

### 随机切换动画

I don't like that the bird keeps shaking its head in a constant loop, it becomes too predictable and mechanic, so let's randomize it a little to make it seem more natural and realistic. So, we'll create a variable in the scene state that indicates which animation we want it to perform. We always want it to keep flapping its wings, of course, so that won't change, but we created two different animations for its head, so let's use them. The variable will have three possible values:

我不喜欢鸟在一个恒定的循环中摇头，这样太可预测和机械，所以得让它随机化一点，使它看起来更自然和逼真。因此，我们将在场景状态中创建一个变量，指示我们希望它执行哪个动画。当然，我们总是希望它不停地拍打翅膀，这个不用改，但我们为它的头部创造了两种不同的动画，所以让我们使用它们。该变量将具有三个可能的值：

* _Null_ will keep its head still

* _Null_ 将保持头静止
  
* _Looking_ will activate the _Bird_look_ animation

* _Looking_ 使用 _Bird_look_ 动画

* _Shaking_ will activate the _Bird_shake_ animation

* _Shaking_ 使用 _Bird_shake_ 动画

We can create a custom type for this variable that only accepts these values.

我们可以为只接受这些值的变量创建自定义类型。

```
export type BirdAction = null | 'looking' | 'shaking'
```

We can then assign this type to a variable when defining it in the scene state, just like you assign `string` or `number` in other cases.

然后，我们可以在场景状态中定义中将此类型赋值给变量，就像在其他情况下指定`string` 或 `number` 一样。

```typescript
export interface IState {
  birdPos: Vector3Component,
  birdAction: BirdAction,
}
//(...)
state: IState = {
  birdPos: {x:5, y:1, z:5},
  birdState: null,
}

```

We want to change the value of this new variable regularly. Let's add it to the same loop that changes the bird's location.

我们想要定期更改这个新变量的值。让我们将它添加到改变鸟类位置的同一循环中。


```typescript
  sceneDidMount() {
    setInterval(() => {
      this.newBirdPos()
      this.newBirdAction()
    }, 4000)
  }
  newBirdAction() {
    let newAction: BirdAction
    const ranNum = Math.random()
    if (ranNum < 0.6){
      newAction = null
    } else if (ranNum < 0.8) {
      newAction =  'looking'
    } else {
      newAction =  'shaking'
    }
    this.setState({birdAction: newAction})
  }
```


To change how our little friend behaves, the last thing we need to do is reference `birdAction` when we render the model.

为了改变我们的小朋友的行为方式，我们需要做的最后一件事是在渲染模型时引用`birdAction`。


```typescript
 async render() {
    return (
      <scene >
        <gltf-model
          src="models/hummingbird.gltf"
          scale={0.2}
          position={this.state.birdPos}
          transition={{
           position: { duration: 500, timing: "ease-in-out" }
          }}
          lookAt={this.state.birdPos}
          skeletalAnimation={[
              { clip: "Bird_fly",
                loop:true, 
                playing:true 
              },
              { 
               clip: "Bird_look", 
               playing: this.state.birdAction == 'looking' 
              },
              { clip: "Bird_shake",
                playing: this.state.birdAction == 'shaking'
              }
          ]}
        />
      </scene>
    )
  }

```

When the statement `this.state.birdAction == 'looking'` evaluates to _true_, then the `playing` property of _Bird_look_ is also _true_. The same applies for _Bird_shake_.

当语句 `this.state.birdAction =='looking'` 计算为 _true_ 时，_Bird_look_ 的 `playing` 属性也是 _true_。这同样适用于 _Bird_shake_。

If we try our scene now, you'll note that the bird sometimes keeps its head still, sometimes it looks around, and sometimes it shakes in what looks like a cute little sneeze.

如果我们现在尝试我们的场景，你会注意到这只鸟有时会保持头部静止，有时会环顾四周，有时它则会打一个可爱的小喷嚏。

### Supporting multiple hummingbirds

### 支持多个蜂鸟

This is where we get to the fun part.

有趣的地方到了。

We have variables that represent the current state of a single bird, but what if we want the same variables to represent the state of multiple birds? We use arrays, that's what we do!

我们有变量代表一只鸟的当前状态，但是如果我们想要相同的变量来表示多只鸟的状态呢？使用数组，我们这样做：

```typescript
export interface IState {
  birdPositions: Vector3Component[],
  birdActions: BirdAction[],
}
// (...)
state: IState = {
  birdPositions:[{x:5, y:1, z:5},{x:5, y:1, z:5},{x:5, y:1, z:5}],
  birdActions:[null, null, null],
}
```

We're adding three sets of values to our arrays for now, and each will produce a separate bird in our scene. Although they all start at the same location, they will soon move apart from each other randomly.

我们现在为数组添加三组值，每个值都会在场景中生成一个单独的鸟。虽然它们都是从同一个位置开始的，但它们很快就会随机分开。

To keep the `render()` function clean, we'll move the rendering of the hummingbird entities away into its own separate function and call it from render like this.

为了保持  `render()`  函数的简洁，我们将把蜂鸟实体的渲染移动到它自己独立的函数中，并从 render 函数中调用它。


```typescript
async render() {
  return (
    <scene>
      {this.renderBirds()}
    </scene>
  )
}
```


The new `renderBirds()` function is very similar to what render used to do, but it goes over the `birdPositions` array using a `map()` operation, creating a new entity for each element in the array. As we iterate through the array, the value stored in the current array position can be referenced through _pos_ and the current index number through _birdNum_.

新的 `renderBirds()` 函数与 render 函数非常相似，但它使用 `map()` 操作遍历 `birdPositions` 数组，为数组中的每个元素创建一个新实体。当我们遍历数组时，存储在当前数组位置的值可以通过 _pos_ 引用，当前索引号可以通过 _birdNum_ 引用。

```typescript
  renderBirds(){
    return this.state.birdPositions.map( (pos, birdNum) =>
      <gltf-model
        src="models/hummingbird.gltf"
        scale={0.2}
        key={birdNum.toString()}
        position={this.state.birdPositions[birdNum]}
        lookAt={this.state.birdPositions[birdNum]}
        transition={{
          position: { duration: 500, timing: "ease-in-out" },
        }}
        skeletalAnimation={[
            { clip: "Bird_fly", 
              loop:true, 
              playing:true 
            },
            { clip: "Bird_look", 
              playing: this.state.birdActions[birdNum] == 'looking'
            },
            { clip: "Bird_shake", 
              playing: this.state.birdActions[birdNum] == 'shaking'
            }
        ]}
      />
    )
  }
```

Notice that now, when we reference variables in the scene state, we refer to a specific indexes in the arrays. We also included a _key_ on each bird entity, this helps the engine keep track of which bird moved where. Without this _key_, the engine would have to guess how the new list of rendered entities corresponds to the one from the last render. That might result in some transitions occurring between positions that were meant to belong to separate birds.

请注意，现在，当我们在场景状态中引用变量时，我们引用数组中的特定索引。我们还在每个鸟类实体上加了一个_key_，这有助于引擎跟踪哪只鸟移动到哪里。如果没有这个_key_，引擎就必须猜测新的渲染实体列表如何与最后一次渲染中的实体对应。这可能会导致在不同鸟类的位置之间产生一些过渡。

We should _always_ change the scene state through the `setState()` function. So to update a single bird we need to set the values for the entire array, even the parts that haven't changed. Here are our `newBirdPos()` and `newBirdAction()` functions, altered to handle arrays:

我们应该_总是_通过 `setState()` 函数改变场景状态。因此，要更新单个鸟，我们需要设置整个数组的值，即使是未更改的部分。这是我们的``newBirdPos()` 和`newBirdAction()` 函数，改为处理数组：

```typescript
newBirdAction(bird: number) {
    let newActions: BirdAction[] = this.state.birdActions.slice()
    const ranNum = Math.random()
    if (ranNum < 0.6){
      newActions[bird] = null
    } else if (ranNum < 0.8) {
      newActions[bird] = 'looking'
    } else {
      newActions[bird] = 'shaking'
    }
    this.setState({birdActions: newActions})
}
  newBirdPos(bird: number) {
    let newPositions = this.state.birdPositions.slice()
    newPositions[bird] = {
      x: (Math.random() *10 ),
      y:  Math.random() *2 + 1,
      z: (Math.random() *10 )
    }
    this.setState({birdPositions: newPositions})
  }
```

Note that in both functions we're making a temporary copy of an array from the scene state, then we change one of the elements in this copied array and finally we pass the whole array as a new value for the variable. When copying the arrays, we use the&nbsp;`.slice()` method to ensure that we're copying the array's values into a new array, rather than just creating a pointer.

请注意，在两个函数中，我们从场景状态创建一个数组的临时副本，然后我们更改此复制数组中的一个元素，最后我们将整个数组作为变量的新值传递。复制数组时，我们使用`.slice（）`方法来确保我们将数组的值复制到一个新数组中，而不是仅仅创建一个指针。

Note that both functions now accept a parameter called _bird_, this determines which of the birds in the arrays to work on. We now need to include a value for this parameter each time we call these functions. Actually, let's go nuts and call both functions a bunch of times manually, just to see how it looks if we have a handful of birds at the same time.

请注意，这两个函数现在都接受一个名为 _bird_ 的参数，这将确定数组中哪些鸟类可以使用。我们现在需要在每次调用这些函数时都包含此参数的值。实际上，让我们疯狂地手动调用这两个函数，只是为了看看我们是否可以同时拥有少量鸟类。


```typescript
  sceneDidMount() {
    setInterval(() => {
      this.newBirdPos(0)
      this.newBirdAction(0)
      this.newBirdPos(1)
      this.newBirdAction(1)
      this.newBirdPos(2)
      this.newBirdAction(2)
      this.newBirdPos(3)
     this.newBirdAction(3)
    }, 4000)
}
```

Now it's time to see if all our changes worked by previewing our scene:

现在是时候通过预览我们的场景来查看我们所有的更改是否有效：

![][24]

Looking good! The biggest problem we have now is that all birds shift positions at the same time. It looks too choreographed, like straight out of a Pixar musical number. We will later be initiating them at different times, which will make it look a lot more natural.

看起来不错！我们现在面临的最大问题是所有的鸟类同时转移位置。它看起来太精心设计，就像皮克斯 Pixar 的音乐编号一样。我们稍后会在不同的时间初始化它们，这将使它看起来更自然。

### Handling a varying number of&nbsp;birds

### 处理不同数量的鸟类

Now let's make things a lot more dynamic!

现在让我们让事情变得更有活力！

We want a new bird to appear in our scene each time you click on a tree. Each time we create a new bird, we want to add a new element to the `birdPositions` and `birdActions` arrays and start a new time-based loop that updates these values periodically.

每次单击树时，我们都希望场景中出现一只新鸟。每次我们创建一只新鸟时，我们想在`birdPositions` 和 `birdActions` 数组中添加一个新元素，并启动一个新的基于时间的循环，定期更新这些值。

The birds start at what seems like a pretty arbitrary set of coordinates, but that's where we'll put our tree.

这些鸟似乎是一组非常随意的坐标，但这就是我们将树放入的地方。

```typescript
 async createBird() {
    this.setState({ 
      birdPositions:[...this.state.birdPositions,{x: 4, y: 2, z: 8}]
    })
    this.setState({ 
      birdActions: [...this.state.birdActions, null] 
    })
    const bird = this.state.birdPositions.length - 1
    setInterval(() => {
      this.newBirdPos(bird)
      this.newBirdAction(bird)
    }, 3000 + Math.random() * 2000)
}
```


We're setting the new values of the state variables by passing the entire array to `setState`, including the values that already existed and didn't change. We're then creating a new loop that will keep calling the newBirdPos and newBirdAction functions for the new bird.

我们通过将整个数组传递给 `setState` 来设置状态变量的新值，包括已存在且未更改的值。然后我们创建一个新的循环，它将继续为新鸟调用 newBirdPos 和 newBirdAction 函数。

We're setting the looping interval with a random number to keep the movements less predictable. Since each bird is created from a user click, we don't have to worry about the birds moving in unison as we saw before. However, if they all looped over the same interval, a predictable repeating pattern would emerge.

我们使用随机数设置循环间隔，以保持移动不可预测。由于每只鸟都是通过用户点击创建的，因此我们不必担心鸟象我们之前看到的一样一致地移动。但是，如果它们都在相同的间隔内循环，则会出现可预测的重复模式。

There'll be no birds in the scene when users first enter it. For this we need to get rid of the initial values that we had manually added to the arrays in the scene state, both should now start empty.

用户首次输入时，场景中不会有鸟类。为此删除我们手动添加到场景状态中的数组的初始值，现在两者都从空开始。

```typescript
state: IState = {
  birdPositions: [],
  birdActions: [],
}
```

Let's now get rid of what we put in `sceneDidMount()` and listen for clicks from the user. When the _tree_ entity is clicked, we will call the `createBird()` function.

现在让我们删除 `sceneDidMount()` 中的内容监听用户的点击。单击 _tree_ 实体时，我们将调用 `createBird()` 函数。


```typescript
 sceneDidMount() {
    this.eventSubscriber.on('tree_click', () => {
    const bird = this.state.birdPositions.length
    if (bird > 10) {return}
      this.createBird()
      console.log("new bird")
    })
  }
```

Each time the user clicks the tree, we're checking the current length of the `birdPositions` array to make sure we don't have too many birds on our scene. In theory, we could keep adding birds forever, but we need to avoid hitting the triangle limit of our scene.

每次用户点击树时，我们都会检查 `birdPositions` 数组的当前长度，以确保我们的场景中没有太多的鸟。理论上，我们可以永远添加，但我们需要避免达到我们场景的三角形限制。

To stand in for a tree, we will just add a box entity and set its id to _tree_. We'll have to pretend that looks like a tree for now.

为了代表树，我们只需添加一个框实体并将其 id 设置为_tree_。我们现在必须假装看起来像一棵树。


```typescript
  async render() {
    return (
      <scene >
        {this.renderBirds()}
        <box
          id="tree"
          position={{ x: 4, y: 2, z: 8 }}
        />
      </scene>
    )
  }
}
```


![][26]

### Adding scenery and animating the&nbsp;tree

### 添加场景并为树提供动画

On this project, I was lucky to get some help from Shibu, our art director here at Decentraland. He built this lovely little landscape and a proper tree to go with it.

在这个项目上，我很幸运能得到 Decentraland 的艺术总监 Shibu 的帮助。他建造了这个可爱的小景观和一棵合适的树。

![][28]

We'll copy both the tree and the rest of the background as _gltf_ models in the `/models` folder of our scene and add two new _gltf-model_ entities to the `render()` function to use the ground and the tree.

我们将树和其余背景作为 _gltf_ 模型复制到场景的 `/models` 文件夹中，并将两个新的 _gltf-model_ 实体添加到 `render()` 函数中以使用地面和树。

We also added an animation to the tree model so that it shakes a little when clicked. This makes it a bit more obvious that something is happening and that the bird is appearing because of the user's action. We added an armature to the tree to do this, just like the hummingbird. Trees with bones… _weird_, but it works.

我们还在树模型中添加了一个动画，以便在单击时稍微摇动一下。
这使得事情变得更加明显，因为用户的行为，鸟出现了。我们在树上添加了一个armature ，就像蜂鸟一样。带 bones 骨头的树...... _有点奇怪_，但有效。

To activate this animation we must add a new boolean variable to the scene state, we'll call it `treeShake`. Each time the user clicks the tree, we want to set this variable to _true_ and then back to _false_ an instant later. We'll create a new function named `shakeTree()` and call it each time the user clicks the tree, right before calling `createBird()`.

要激活此动画，我们必须在场景状态中添加一个新的布尔变量，我们称之为`treeShake`。每次用户单击树时，我们都希望将此变量设置为 _true_，然后稍后再返回 _false_ 。我们将创建一个名为 `shakeTree()` 的新函数，并在每次用户单击树时调用它，在调用 `createBird()` 之前。


```typescript
  async shakeTree(){
    this.setState({treeShake: true})
    setTimeout( f => {
      this.setState({treeShake: false})
    }, 2000)
  }
```

Here we're using a `setTimeout()` function to delay the action of setting `treeShake` back to _false_ by 2000 milliseconds.

这里我们使用 `setTimeout()` 函数将 `treeShake` 设置为 _false_ 的动作延迟2000 毫秒。

### Coding tip of the day: never set a scene state variable&nbsp;directly

### 编程提示：永远不要直接设置场景状态变量

In this example you've seen that we always made changes to our scene state through `setState()`, even when passing a whole array. While it's possible to set a variable or one of its array elements directly, and you might get away with it, try to avoid this at all costs.

在这个例子中，您已经看到我们总是通过 `setState()` 对场景状态进行更改，即使在传递整个数组时也是如此。虽然可以直接设置变量或其中一个数组元素，您可能会侥幸成功，但请不惜一切代价避免这种情况。

In our scene, there were a number of times where it would have been tempting to just write `this.state.birdPositions[bird] = newPos`. The trouble is that this could potentially mess up how the scene object keeps track of changes, especially when there are multiple threads running in parallel that each have an effect on the scene state.

在我们的场景中，有很多次尝试只写 `this.state.birdPositions[bird] = newPos`。麻烦的是，这可能会使场景对象对变化的跟踪弄乱，特别是当有多个线程并行运行时，每个线程都对场景状态产生影响。

Using the `setState()` function to change variables also has the added bonus that it calls the `render()` function automatically to display the scene in its new state. Remember that unlike most game engines out there, scenes in Decentraland aren't rendered in a continuous loop. They are only rendered once something in scene is known to have changed.

使用 `setState()` 函数来改变变量也有额外的好处，它会自动调用 `render()` 函数来显示处于新状态的场景。请记住，与大多数游戏引擎不同，Decentraland 中的场景不以连续循环来显示。只有在已知场景中的某些内容发生变化时才会渲染它们。

### Final thoughts

### 最后的想法

![][30]

As we've learned today, you don't need to explicitly define every single entity in your scene as a literal XML tag in the render function. You can build entities from an array if you use them cleverly.

正如我们今天所了解的那样，您不需要将场景中的每个实体显式定义为 render 函数中的文字 XML 标记。您可以巧妙地使用数组来构建实体。

Play around with your array lengths and values to completely transform your scene over time. This idea is essential for building games, where you often have to handle similar arrays for enemies, obstacles, collectible items, features of a dynamic scenery, etc. You'll also find that many other interactive experiences in addition to games can benefit from this kind of mechanic. [Feel free to play with any of the code we've included in the example in GitHub!][9]

随着时间的推移，使用您的数组长度和值来完全转换您的场景。这个想法对于构建游戏至关重要，你经常需要为敌人，障碍物，收藏品，动态风景的特征等处理类似的数组。你还会发现除了游戏之外还有许多其他互动体验可以从这种机制中受益。 [请随意玩弄我们在 GitHub 的示例中包含的任意代码！][9]

Thanks for following along, and stay tuned for our next Developer Tutorial!

感谢您的关注，并请继续关注我们的下一个开发人员教程！





[1]: https://cdn-images-1.medium.com/freeze/max/30/0*cP0UGeoiXqpGr7B7?q=20
[2]: https://cdn-images-1.medium.com/max/2000/0*cP0UGeoiXqpGr7B7
[3]: http://docs.decentraland.org
[4]: https://github.com/decentraland/documentation
[5]: https://blog.decentraland.org/build-your-first-interactive-scene-using-the-sdk-5d6895ac78f0
[6]: https://reactjs.org/
[7]: https://cdn-images-1.medium.com/freeze/max/30/0*vnV93ywFpivCAnSv?q=20
[8]: https://cdn-images-1.medium.com/max/800/0*vnV93ywFpivCAnSv
[9]: https://github.com/decentraland/sample-scene-array-of-entities
[10]: https://poly.google.com/view/70NyKFt-vLF
[11]: https://creativecommons.org/licenses/by/2.0/
[12]: https://www.blender.org/
[13]: https://cdn-images-1.medium.com/freeze/max/30/0*bUzVGe1IpYIA9MXK?q=20
[14]: https://cdn-images-1.medium.com/max/800/0*bUzVGe1IpYIA9MXK
[15]: https://cdn-images-1.medium.com/freeze/max/30/0*k1gnkaKWBPhTvsy0?q=20
[16]: https://cdn-images-1.medium.com/max/800/0*k1gnkaKWBPhTvsy0
[17]: https://github.com/Kupoman/blendergltf
[18]: https://docs.decentraland.org/documentation/create-scene/
[19]: https://cdn-images-1.medium.com/freeze/max/30/0*XuKi3HBiHUc7U3c4?q=20
[20]: https://cdn-images-1.medium.com/max/800/0*XuKi3HBiHUc7U3c4
[21]: https://cdn-images-1.medium.com/freeze/max/30/0*zGxs0Sb_kcXgJc4C?q=20
[22]: https://cdn-images-1.medium.com/max/800/0*zGxs0Sb_kcXgJc4C
[23]: https://cdn-images-1.medium.com/freeze/max/30/0*oKmy9EAiHWd4HNeP?q=20
[24]: https://cdn-images-1.medium.com/max/800/0*oKmy9EAiHWd4HNeP
[25]: https://cdn-images-1.medium.com/freeze/max/30/0*HToGYEphsUlJs4Vi?q=20
[26]: https://cdn-images-1.medium.com/max/800/0*HToGYEphsUlJs4Vi
[27]: https://cdn-images-1.medium.com/freeze/max/30/0*ss1gWR3v97fotQI-?q=20
[28]: https://cdn-images-1.medium.com/max/800/0*ss1gWR3v97fotQI-
[29]: https://cdn-images-1.medium.com/freeze/max/30/0*fl1cYv8Ms7D5NfiX?q=20
[30]: https://cdn-images-1.medium.com/max/800/0*fl1cYv8Ms7D5NfiX
[31]: https://discordapp.com/invite/9EcuFgC
[32]: https://developers.decentraland.org
[33]: https://twitter.com/decentraland
[34]: https://www.reddit.com/r/decentraland/
[35]: https://t.me/DecentralandTG
[36]: https://developers.decentraland.org/
