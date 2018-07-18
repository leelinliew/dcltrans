Hello, in this tutorial I’ll show you how to use the CLI to create a new decentraland scene to edit it preview it and upload it to ipfs.

大家好，在本教程中，我将向您展示如何使用 CLI 创建一个新的 decentraland 场景，以及如何编辑、预览并将其上传到 ipfs。

so first we create a folder where all the file of your scene will be store.

所以首先我们创建一个文件夹，场景的所有文件都在放在这个目录中。

then we initialize the scene using DCL init and answer a few auestions, the scene title describes your scene ,the eth address is optional but it is useful when deploying the scene.

然后我们使用 DCL init 命令来初始化场景，然后回答它的几个问题，如用来描述你的场景的标题，以太地址是可选的，但会在部署场景时用到它。

the name and mail are optional too but are useful to get contacted， the parcels are used to define the build area and in the upload process.

名字和邮件也是可选的，用于方便联系，地块坐标用于定义构建内容的区域范围并会在上传过程中用到。

this scene will only have static elements so we chose static scene project ,the next step can take some time depending on your computer and your connection,

这个场景只用静态元素，所以我们选择静态场景项目，下一步可能需要一些时间，具体取决于你的计算机速度和网速，

it’s downloading and installing all of the dependencies, once the installation is done we can open the file in a text editor,

它正自动下载并安装所有依赖项，一旦安装完成，我们可以在文本编辑器中打开文件。

in this case I’ll use Visual Studio code ,and I open the file scene.XML.

这里，我将使用 Visual Studio code，并打开文件 scene.xml。

this file contains all the data of your static scene. before editing it we will open the preview of our scene, to do that open a terminal and type dcl preview ,this will open the preview in our browser and we will be able to explore.

此文件包含静态场景的所有数据。在编辑它之前，我们将打开场景预览，打开终端并输入 dcl preview，它会在浏览器中打开预览，方便我们探索虚拟3D世界。

we can for example change the radius of this yellow cylinder , or its position. then we will remove the pink sphere and replace it by a model of a thumbs up, to do that we have to create a new element named gltf model set its source to our gltf 3d file the positon and the scale.

例如，我们可以改变这个黄色圆柱的半径或它的位置。然后我们将删除粉红色的球体并用拇指的模型替换它，为此我们必须创建一个名为 gltf-model 的新元素，将其来源设置为我们的 gltf 3d 文件.

in this case we will place the model on the green plane and lower the scale because the original size of the model is big,

设置 position 和 scale，在这种情况下，我们将模型放在绿色平面上并降低比例，因为模型的原始尺寸很大，

don’t forget to close the element like this , I’ll copy my model into our folder, gltf models contain a gltf file and a bin file ,we can see the model in your preview.

像这样，不要忘记关闭元素。我将我的模型复制到我们的文件夹中，gltf 模型包含一个 gltf 文件和一个 bin 文件，我们可以在预览中看到模型。

we will remove the box to get a more clear view.

我们将删除这个盒子以获得更清晰的视图。

we will upload our scene to ipfs. you have to install ipfs first and get the daemon running ,then we go in a terminal in our project folder and type DCL deploy, we can verify if all the files are correct then type Y and press Enter,

我们将我们的场景上传到 ipfs。你必须首先安装 ipfs 并运行守护进程，然后我们进入项目文件夹中的终端并键入 dcl deploy，我们可以验证所有文件是否正确，然后键入 Y 并按回车键，

once the files are uploaded to ipfs ,we will get of IP NS address and a page will open to link the IPNS hash to our Decentraland using metaMask.

一旦文件上传到 ipfs，我们就能获得 IPNS 地址，并打开一个页面，使用 metaMask 将 IPNS 哈希链接到我们的 Decentraland。