## IDEA的好用插件推荐
### JRebel for IntelliJ
一款热部署插件，只要不是修改了项目的配置文件，用它都可以实现热部署。收费的，破解比较麻烦。不过功能确实很强大。算是开发必备神器了。热部署快捷键是control+F9/command+F9。

### .ignore
git提交时过滤掉不需要提交的文件，很方便，有些本地文件是不需要提交到Git上的。

### CamelCase
将不是驼峰格式的名称，快速转成驼峰格式，安装好后，选中要修改的名称，按快捷键shift+alt+u。

### Lombok plugin
开发神器，可以简化你的实体类，让你i不再写get/set方法，还能快速的实现builder模式，以及链式调用方法，总之就是为了简化实体类而生的插件。
### Mybatis plugin
可以在mapper接口中和mapper的xml文件中来回跳转，就想接口跳到实现类那样简单。

### codehelper.generator
可以让你在创建一个对象并赋值的时候，快速的生成代码，不需要一个一个属性的向里面set,根据new关键字，自动生成掉用set方法的代码，还可以一键填入默认值。

> GenAllSetter 特性

在Java方法中, 根据 new 关键词, 为Java Bean 生成所有Setter方法。
按GenAllSetter键两次, 会为Setter方法生成默认值。
可在Intellij Idea中为GenAllSetter设置快捷键。
如何使用:
将光标移动到 new 语句的下一行。
点击主菜单Tools-> Codehelper-> GenAllSetter, 或者按下GenAllSetter快捷键。
GenDaoCode 特性

- 根据Pojo 文件一键生成 Dao，Service，Xml，Sql文件。
- Pojo文件更新后一键更新对应的Sql和mybatis xml文件。
- 提供insert，insertList，update，select，delete五种方法。
- 能够批量生成多个Pojo的对应的文件。
- 自动将pojo的注释添加到对应的Sql文件的注释中。
- 丰富的配置，如果没有配置文件，则会使用默认配置。
- 可以在Intellij Idea中快捷键配置中配置快捷键。
- 目前支持MySQL + Java，后续会支持更多的DB。

#### GenDaoCode 使用方法

**主菜单Tools-> Codehelper-> GenDaoCode 按键便可生成代码。**

- 方法一：点击GenDaoCode，然后根据提示框输入Pojo名字，多个Pojo以 | 分隔。

Codehelper Generator会根据默认配置为您生成代码。

- 方法二：在工程目录下添加文件名为codehelper.properties的文件。

点击GenDaoCode，Codehelper Generator会根据您的配置文件为您生成代码

### GsonFormat
一键根据json文本生成java类  非常方便

### GenerateAllSetter
一键调用一个对象的所有set方法并且赋予默认值 在对象字段多的时候非常方便，在做项目时，每层都有各自的实体对象需要相互转换，但是考虑BeanUtil.copyProperties()等这些工具的弊端，有些地方就需要手动的赋值时，有这个插件就会很方便，创建完对象后在变量名上面按Alt+Enter就会出来 generate all setter选项。

### CodeGlance
在编辑区的右侧显示的代码地图。

## 下面几个是装X神器了（让你的开发工具变得靓丽起来）
### Material Theme UI(这个最牛了，撸代码的时候感觉前面就像是你的女朋友一样，美丽动人，嘻嘻嘻)
这是一款主题插件，可以让你的ide的图标变漂亮，配色搭配的很到位，还可以切换不同的颜色，甚至可以自定义颜色。默认的配色就很漂亮了，如果需要修改配色，可以在工具栏中Tools->Material Theme然后修改配色等。

### Background image Plus
这是一款可以设置idea背景图片的插件，不但可以设置固体的图片，还可以设置一段时间后随机变化背景图片，以及设置图片的透明度等等。

### activate-power-mode
这是一款让你在编码的时候，整个屏幕都为之颤抖的插件。

### Nyan progress bar
这是一个将你idea中的所有的进度条都变成萌新动画的小插件。

### Rainbow Brackets
彩虹颜色的括号  看着很舒服 敲代码效率变高