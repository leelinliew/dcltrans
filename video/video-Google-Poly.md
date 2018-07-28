How to import a google poly model into a decentraland scene

如何将 google poly 模型导入到 decentraland 场景中

hi, welcome to the tutorial on how to import a Google poly model into a decentraland scene. let's get started, so Google poly is a platform offered by Google that allows you to browse , discover and download 3d objects to your scene in a quick and easy manner. you're free to search through the featured content and search for what you'd like to put in your scene. however I found that the quickest way to actually go to the top and search for exactly what you're looking for.

嗨，欢迎来到如何将 Google poly 模型导入 decentraland 场景的教程。让我们开始吧，Google poly 是 Google 提供的一个平台，它能让您快速简便的方式浏览、发现和下载 3D 对象到您的场景。您可以自由浏览内容推荐，查找您想要放置在场景中的内容。然而，我发现实际上最快的方式是用搜索来寻找的你所需要的东西。

in our case let's search for rocket, ok and as you can see you have a wide range of objects to choose from, I'm interested in this Val condign rocket here, no , it's nice is you have a 3d view that within the browser that allows you to look at the 3d object from different angles,

在这个例子中，让我们搜索火箭，好吧，你可以看到你有各种各样的物体可供选择，我对这个 Val condign 火箭感兴趣，在浏览器中有一个 3d 视图,您可以从不同角度查看 3d 对象。还真是不错。

so you can make sure it's exactly what you want before downloading, now to download all you have to do is click search for the download button underneath this 3d window, and you have a few file format options to choose from, now before we download make sure you're aware of the license terms and conditions and be sure that you give the author credit if needed, let's go ahead and download, since we want to edit this object, I'm going to download in an obj file format.

你可以在下载之前确保它正是你想要的，你只要点击 3d 窗口下面的下载按钮就可以下载，还可以选择下载文件的格式，下载之前先确认下许可条款，并确保你在必要时给作者付款，让我们继续，下载，因为我们要编辑这个对象，所以我使用 obj 文件格式下载。

okay so locate the file wherever you choose to download it, unzip it with your favorite unzipping software, it can be WinZip or 7-zip, however on Mac OS you simply double click to unzip, once you open the unzip file you will see that you have your obj file format or whichever you chose to download. great so now we're ready to go , into blender now, our goal is to bring this object that we just downloaded it into our Dcentraland insane, in order to do that, it will need to be in a format called GLTF. if we click on file and we click export before we do anything in blender, you'll notice that we have all these file formats but gltf is not present.

不错，找到你下载的文件，用你最喜欢的解压缩软件解压，如 WinZip 或 7-zip，但在 Mac OS 上你只需双击解压缩，打开解压缩文件后，你就会看到 obj 文件或任何你选择下载的格式。好了，现在我们已经准备好了，打开 blender，我们的目的是将我们刚下载的这个对象导入到我们的 Decentraland 场景中，为了做到这一点，需要一种名为 GLTF 格式的文件。如果我们点击文件菜单，并在我们在 blender 中执行任何操作之前单击 export，您会看到所有支持的文件导出格式，但是其中并没有 gltf。

so to solve that problem, we need to head on over to Google and let's type gltf sorry blender, and it's gonna be the first link that appears, look for the clone and download button and select download zip, the file size is actually pretty large and may take a while to download, depending on your internet connection. I've already downloaded and unzipped this file, and I have located it right here.

为了解决这个问题，我们打开 Google， 并输入 gltf ，抱歉， blender。应该是第一个出现的链接，找到 clone and download 按钮并选择下载 zip，这个文件实际上比较大，可能需要一段时间才能下载，具体取决于您的互联网连接。我已经下载并解压缩了这个文件，就在这里。

let's head back to blender now, in blender after we have unzipped our gltf file that we downloaded, we need to go to file, user preferences and now we look for scripts, and click on the folder to the right of scripts, let's locate that gltf file that we downloaded earlier, ok once you've located the file go ahead and click on that folder, go into scripts and click accept. now let's save our user settings, great we can now close out of the bring up blender user preferences, let's actually close out of the blender application altogether as our settings need to update now , when we reopen blender we can go to file export and we will see our gltf export option along with this GLB export option.

让我们现在回到 blender，在我们解压缩了我们下载的 gltf 文件后，在 blender 中，我们需要选择 “file” ，“user preferences”，找到 “scripts” 项，然后单击“scripts”右侧的文件夹按钮，找到我们之前下载的 gltf 文件，找到文件后继续单击该文件夹，进入“scripts”目录，然后单击“accept”。现在保存我们的用户设置，好，我们现在可以关闭 blender 用户首选项，让我们关闭 blender 应用程序，因为我们的设置需要现在更新，当我们重新打开 blender 时，我们可以打开“文件->导出”菜单，我们就能看到 gltf 的导出选项以及这个 GLB 导出选项。

for today's tutorial we're interested in the gltf file format, now we're ready to import our object that we downloaded from google Poly, to do so let's go to file import and select the file format that you chose when downloading your file from Google Poly.

对于今天的教程来说，我们对 gltf 文件格式感兴趣，现在我们已准备好导入我们从 google Poly 下载的对象，为此我们选择“文件->导入”菜单，选择我们在 google poly 中下载文件时选择的文件格式。

in my case I chose the obj file format or the wavefront file format, so I'm gonna select that. let's go ahead and locate our file that we downloaded, mine should be saved to the desktop, there it is. now once you've located that file, go ahead and click on import obj or whichever format you chose.

在当前情况下，我选择了 obj 文件格式或 “wavefront” 文件格式，所以我要选择它。继续，找到我们下载的文件，我的文件应保存到桌面，就在那里。现在，一旦找到该文件，继续点击导入 obj 或您选择的任何格式。

great now we see our objects actually quite large, so to get rid of this cube, let's go ahead and right-click on it to select it. press the X key and then select delete, let's say we want to change these engines here, so we can actually right click again to select the engines, click on the s key to change the scale, let's say we want some crazy large alien-looking rocket thrusters , let's press the s key drag the mouse away from the object, until you get to the desired scale, then click to release, now all this simply did was change the scale and increase the scale of our rocket engines.

好，现在我们看到我们的对象实际上非常大，为了删除这个立方体，让我们继续，右键单击它来选择它。按 X 键然后选择删除，假设我们想更改这里的这些引擎，我们可以再次右键单击选择引擎，点击s 键更改缩放比例，假设我们需要大型外星火箭推进器，按下 s 键将鼠标拖离物体，直到达到所需的比例，然后点击释放，所做这些简单操作，是为改变了缩放比例并增加了火箭发动机的大小。

let's do something interesting with it. go into edit mode and we can actually select push and pull, now drag the mouse away from the object or towards it to get your desired outcome. let's go towards it, it might be a little too large, let's change the scale so to change the scale one more time, you press the S key , and if you're trying to decrease in size go towards the object, and if you're trying to increase in size, go away from it. that's a good size there we could also shrink and flatten to get cooler effects. I'm satisfied with that.

让我们做一些更有趣的事情。进入编辑模式，我们就可以选择 “push and pull”，现在将鼠标拖离对象或朝向它，以获得您想要的结果。让我们走向它，它可能有点太大，让我们改变比例，为再次改变比例，按 S 键，如果你想减小尺寸，移向对象，如果试图增加大小，远离对象。这是一个合适的大小，我们也可以收缩和变平，以获得更酷的效果。我对现在的效果很满意。

okay so let's zoom out, excellent, so let's say we're satisfied with our model 2x plus, go to file export and select the gltf 2.0 file format, let's go ahead and give a name, you're gonna name it rocket, ok now let's select where to save it, actually you want to save this file in the same directory in which your decentraland scene file is located. so in my case I have mine saved in this directory. I'm going to put my model into a folder called models, and then select export,

好吧，让我们缩小，非常好，我们对我们 2 倍多大的模型感到非常满意，选择“文件->导出”菜单并选择 gltf 2.0 文件导出格式，接着给它一个名字，你可能命名为火箭，好吧，现在让我们选择保存的位置，实际上你想将这个文件保存在你的 decentraland 场景文件所在的目录中。我的情况是保存在此目录中。我要把我的模型放到一个名为 models 的文件夹中，然后选择 “export”，

great now let's open up our directory in which our scene resides on.ok so once you're in your directory, go ahead and locate your scene file if you created a static scene like I did, go ahead and look for scene dot xml and open it now.

不错，现在打开我们的场景所在的目录。好，已经进入到目录中，如果你像我一样创建的是静态场景，请继续找到你的场景文件，找到 scene.xml 文件并打开。

when you first open the scene you might notice some different code in between the syntax here, if so go ahead and delete that section. now let's head on over to the center lens documentation, to get there go to Doc's dot decentraland org and let's select SDK reference, now under SDK reference if we click on scene content guide, we will see some examples explanations in sample code, force scroll down until you see import 3d models, here's the appropriate syntax for our situation, since we're using the gltf file format you will notice the gltf-model tag and you will see the position category, and you can change the x y and z values, you have the ability to change scale and your source is where you input the name of your file, and if it's enclosing folder let's go back to our IDE,

当您第一次打开场景时，您可能会注意到这里的语法之间有一些不同的代码，如果是这样，请删除该部分。现在让我们转到中心文档，打开 docs.decentraland.org, 选择 SDK 参考，现在在 SDK 参考下，如果我们点击“场景内容指南”，我们将在示例代码中看到一些示例解释，滚动到你看到“导入 3d 模型”，这是我们这个情况下适用的语法，因为我们使用 gltf 文件格式，你会注意到 gltf-model 标签，你会看到 “position” 项，你可以改变 x y 和 z 值，可以改变 scale，src 就是你输入文件名的地方，如果它是封闭文件夹，让我们回到我们的编辑器。

okay so if you would like to make your edits, let's say you want to change a long position this is your x axis, y axis and z axis, the same is true for scale. before we run the commands to preview our scene, make sure that you save your scene file in your IDE.

好吧，如果您想进行编辑，假设您要更改位置，这是 x 轴，y 轴和 z 轴，对于 scale 也是如此。在我们运行命令预览场景之前，请确保将场景文件已在编辑器中保存。

ok so in order to run that scene, let's go ahead and open terminal or command prompt depending on your operating system. the command to preview a scene is DCL preview, let's go ahead and press ENTER, and see what happens. excellent, so now you can see, we can click on it navigate around and there's our object, so there you have it. how to import a model from Google poly, bring it into blender and edit, export and upload to your descent.

好吧，为了运行场景，让我们继续，打开“终端”或“命令提示符”，具体取决于您的操作系统。预览场景的命令是 dcl preview，让我们继续并按 ENTER 键，看看会发生什么。非常好，现在你可以看到，我们可以点击它，四处走动，这就是我们的对象。这里我们知道了如何从 Google poly 导入模型，将其导入 blender 并编辑，导出并上传到您的 decentraland。