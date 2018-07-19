hi there my name is Ryan and in this video we're taking a look at what it takes to download a model from sketchfab, edit it in blender and put it finally into our decentraland scene.

嗨，我是 Ryan，在这个视频中，我介绍一下如何从 sketchfab 下载模型，如何在 blender 中编辑，最后如何将它放到我们的 decentraland 场景中。

for this video on top of our Decentral and IDE, we're gonna need a copy of blender and a copy of the gltf blender exporter a plug-in that goes alongside blender, let's start by installing the gltf blender plugin, with 7-zip let's navigate into the gltf blender exporter file and look for a folder under scripts and add-ons, we're looking for the IO scene gltf to file.

对于这个视频，除了我们的 decentraland 和 IDE 之外，我们还需要一个 blender 应用及 gltf blender exporter，一个与 blender 一起使用的插件，首先我们安装 gltf blender 插件，在 7-zip 中，我们导航到 gltf blender exporter， 查找 scripts 和  addons 文件夹，我们正在寻找是 io_scene.gltf 文件。

now let's open our windows, navigate to our install path of blender, and from here go into our version scripts and add-ons folder, let's drag this folder into our path, I've already installed it, so let's skip it. once it's installed we're ready to go.

现在让我们打开资源管理器窗口，导航到我们的 blender 安装路径，然后从这里进入版本，scripts, addons 文件夹，让我们将这个文件夹拖到我们的路径中，我已经安装过了，所以让我们跳过。一旦安装完毕，我们就准备好了。

let's find the model that we're gonna use on sketchfab, I found a patch of heaven this little white tree, that's actually kind of red is gonna be in our Decentraland scene, very soon, I've already gone ahead and downloaded it. but if you haven't take a look and download it on the bottom left here, once you get download you'll be prompted with two options, an original format which is an obj file or an auto converted format which in this case is a gltf file, which directly inputs into decentral. and since we have some changes to make we're gonna leave it in the original format.

让我们找到我们将在 sketchfab 上使用的模型，我找到了一个模型： “Patch of Heaven - The White Tree”，实际上它是红色的，它将出现在我们的 Decentraland 场景中，很快，我已经开始下载它了。但如果您还没有，看一下左下角的下载按钮，点下载后，您将会看到两个选项，一个是 obj 文件的 original format,，另一个是 auto converted format，在这种情况下是 gltf 文件，它可以直接导入 decentraland。因为我们要做一些修改，所以我们选择 original format 下载。

but if you're satisfied with the white tree in its original existence, go ahead and download the gltf file, and leave it be once you have the file downloaded, extract it and we'll see what we're working with, we have two files textures and source. for our purposes, we're gonna be going into source and we will encounter another where our archive use 7-zip or your favorite file extractor to extract it.

但如果您对目前的这个白树感到满意，请下载 gltf 文件，并在下载文件保存，将其解压缩，我们将看到我们要处理的文件，我们有两个目录，textures 和 source，为了我们将进入 source，我们将遇到另一个压缩文件，使用 7-zip 或您喜欢的解压缩工具来解压缩。

let's go in again in this folder will have textures and our 3d object files which is what we need. let's boot up blender and first, enable our gltf plugin under user preferences and add-ons, go ahead and search gltf on my machine, i've already enabled it but since you've just installed it, check it and will then be good to go.

让我们再次进入这个文件夹，这是我们需要的纹理文件和 3d 对象文件。让我们启动blender，首先，在用户首选项和附加组件下启用我们的 gltf 插件，继续在我的机器上搜索 gltf，我已经启用它了，但是因为你刚安装它，请检查一下以便下一步操作。

once we have the plug-in enabled, let's get rid of this disgusting cube, and import our tree, since it's an obj file we're gonna hit import wavefront and we're gonna import our obj file, it's quite large, so we're gonna have to scale it down in our Decentraland scene.

一旦我们启用了插件，让我们删除这个的立方体，然后导入我们的树，因为它是一个 obj 文件，我们点击 import wavefront，导入我们的 obj 文件，它非常大，所以我们我们必须在我们的 Decentraland 场景中缩小它。

but first let's get to editing, I really don't like the shape of the trunk even though it's very beautiful, I'm gonna right-click on the trunk to select it, and then hit tab to enable editing mode, from here I'm going to right click to deselect, and then lasso tool with ctrl + click and edit some of the trunk.

但首先让我们开始编辑，我真的不喜欢树干的形状，即使它很漂亮，我要右键单击树干来选择它，然后按 Tab 键启用编辑模式，从这里我我要右键单击取消选择，然后用 ctrl + 点击套索工具编辑一些树干。

once we're satisfied with our huge edits were ready to export, under file export we have the option to export as a gltf or jail B file, I'm gonna export as a gltf, on the desktop blender has exported seven files for us, an untitled dot bin an untitled gltf and five other texture files.

一旦我们对编辑感到满意就准备导出，在文件，导出下我们可以选择导出选项： gltf 或 jlb 文件，我将导出为 gltf，blender 为我们在桌面上导出了 7 个文件，一个untitled.bin，untitled.gltf 和其他五个纹理文件。

to make things simple let's drag these into our root directory, and then open our scene XML, in our scene XML we have four pre-existing shapes, let's delete them and add our gltf model to call our GFTL model, gfTL - model will start our tag, now we can add a source which in our case is untitled gltf,

为了简单起见，让我们将它们拖到我们的根目录中，然后打开我们的 scene.xml，在我们的scene.xml 中我们有四个预先存在的形状，让我们删除它们，添加我们的 gltf模型， 为了调用我们的 gltf 模型，输入 gltf-model 标签，现在我们可以添加一个源，在我们的例子中是 untitled.gltf,

I made a typo here and since it's large, we're gonna scale it down to 0.1 0.1 0.1, I'm also going to give it an ID and then finish off our call. if we open up command prompt and navigate to our directory and then preview our decentraland scene, we will have our tree now,

我在这里打错了，因为它很大，我们要把它缩小到 0.1 0.1 0.1，我还给它一个 ID，然后结束我们的调用。如果我们打开命令提示符并导航到我们的目录，然后预览我们的 decentraland 场景，我们现在有了我们自己的树，

in this case we didn't do the best job of scaling, but we have shown how to take a model from sketchfab and put it into a decentralized scene, if you have any questions please refer to the docs at Doc's Decentral and org or post on our subreddit reddit.com  deCentral and thanks for watching, I'll see you again next time.

在这种情况下，我们并没有调整到最好，但我们已经展示了如何从 sketchfab 中获取模型并将其放入 decentraland 场景中，如果您有任何疑问，请参阅 docs.decentraland.org 上的文档或 reddit.com r/decentraland 上的帖子，感谢收看，我下次再见。
