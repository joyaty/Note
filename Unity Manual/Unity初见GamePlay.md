# Creating GamePlay

Unity提供了许多元素来辅助创建GamePlay，比如场景（Scene），游戏对象（GameObject），预制件（Prefab）等等。

------

### Scene

可以简单的把Scene看做一个游戏关卡，在场景中，可以放置各种元素，比如地图物件，可控制单位，AI单位，环境光照等等。当创建一个空的Unity项目时，Unity会自动创建一个场景，包含和一个相机和平行光照组件。

------

### GameObject

GameObject是Unity中非常重要的一个概念。游戏世界中的任何对象都可以看做GameObject，比如可控制单位，光照，相机以及各种特效等等。GameObject本身不实现任何功能，它是一个容器，通过指定各种Component来赋予GameObject具体的功能。

Transform是每个GameObject都具有的Component，用于保存GameObject的Position、Rotation、Scale信息，这样GameObject就能够放置在游戏世界具体的位置上，并且有自己的旋转和缩放。Transform组件无法从GameObject上移除，并且在具有父子关系的GameObject层级上，Transform组件有着同样的父子关系，Transform组件上保存的总是本地坐标系的信息，可以通过父子关系和矩阵变化，获取GameObject的世界坐标系下的Transform信息。

Unity内置了许多类型的GameObject，如Camera，Light，各种简单图元（如Cube，Sphere，Plane等等）。这些GameObject都由Transform组件以及各个GameObject相关的功能Component组成，比如Camera组件，Light组件，各种图元的MeshRender组件。脚本（Script）也是一个特殊的组件，我们可以通过编写Script，在GameObject上处理一些自定义的游戏逻辑。

GameObject的各个Component，包括Script，可以配置各种Property（属性），用于指定Component的行为参数。包括了两种Property，分别为Value Property（值属性）和Referance Property（引用属性），Value Property直接保存一个值，而Referance Property可指向一个资产配置等，比如MeshRender中，Material可以指向Assets中的一个Material资源。

还可以给Unity指定Tag，我们可以通过Tag方便的在Script中访问和定位具有这个Tag的一个或多个GameObject。Unity内置了一些Tag，我们也可以通过**Add Tag...**来添加自定义Tag，注意，一旦创建了Tag，后续无法重命名。

```c#
GameObject.FindWithTag("TagName");
```

如果一个GameObject在运行时是不会移动的，我们可以指定这个GameObject是Static的，否则就是dynamic的。对于一个Static的GameObject，Unity可以预先计算这个GameObject的相关信息，因为不会移动，因此预计算的信息在运行时同样适用，可以节约运行时的效能。![2.GameObjectStaticDropDownMenu1](C:\WorkSpace\Note\Unity Manual\images\2.GameObjectStaticDropDownMenu1.png)

如上图所示，可以在Inspector窗口中指定GameObject是否是Static，并且Unity提供了许多支持Static GameObject预计算的内置系统，可以通过在下拉列表选择Unity各个内置如何预计算该GameObject。**基于效能考虑，应该只勾选会处理这个GameObject的Unity System，否则可能会产生计算浪费、不需要的数据以及一些未知的行为**。

------

### Prefabs

Unity的Prefab系统允许创建、配置、保存一个GameObject对象以及配置在GameObject的各种Component、Property和Child GameObject。Prefab可以作为一个可复用资产，在场景中使用Prefab作为模板创建新的实例。