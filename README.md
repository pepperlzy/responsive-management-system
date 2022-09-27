# 项目重点

## 确定响应式断点

## 确定适配方案-以PC端为主

> 网页按照PC端进行布局,然后过渡到不同尺寸
> 
## 分配页面所占比例

## 核心部分

### 头部导航栏在屏幕宽为768px收缩点击显示与隐藏

```javascript
 // 头部导航模块
    // 获取J_nav
    var J_nav = document.getElementById("J_nav");
    var J_nav_list = document.getElementById("J_nav_list");
    // console.log(J_nav, J_nav_list);
    J_nav.onclick = function () {
      // 点击时添加类名，再次点击删除类名
      J_nav_list.classList.toggle("sm-ul-show");
    };
```

### 侧边栏的展开与收缩效果

> 侧边栏宽屏下点击展开子类项目,1400px下侧边栏收缩

![1661168153067](https://user-images.githubusercontent.com/109357565/192475461-070fe78d-895d-408a-9582-6402f946c265.png)

![1661168153067](https://user-images.githubusercontent.com/109357565/192475503-0f668446-f7d1-4331-b52d-573cba8b20a4.png)

> 点击展开

![1661168375359](https://user-images.githubusercontent.com/109357565/192475525-e5f83956-38e2-4c62-9149-d214cae5bedf.png)

核心功能代码

```javascript
  // 侧边导航栏
    // 获取标题
    var menuTitles = document.querySelectorAll(
      "#J_menu .menu-list .menu-list-title"
    );
    var J_menu = document.getElementById("J_menu");
    // console.log(menuTitles);
    var len = menuTitles.length;
    for (var i = 0; i < len; i++) {
      // 给每个menuTitles添加flag属性
      menuTitles[i].flag = "hidden";
      menuTitles[i].onclick = function () {
        // 属性值为hidden,给当前menuTitles添加menu-list-title-active类名
        if (this.flag === "hidden") {
          // 全屏时点击
          this.classList.add("menu-list-title-active");
          // 获取兄弟元素的高
          var h = this.nextElementSibling.clientHeight;
          // console.log(h);
          // 设置当前元素的父元素高度
          this.parentNode.style.height = h + 40 + "px";

          // 缩小情况下再点击,修改侧边栏宽度为260px
          J_menu.style.width = "260px";
          // 将当前属性值hidden修改为show
          this.flag = "show";
        } else {
          // 属性值为show,给当前menuTitles删除menu-list-title-active类名
          this.classList.remove("menu-list-title-active");
          // 设置当前元素的父元素高度
          this.parentNode.style.height = "40px";
          // 将当前属性值show修改为hidden
          this.flag = "hidden";
        }
      };
    }
    // 添加浏览器窗口监听事件
    window.addEventListener("resize", function () {
      // 动态获取当前屏幕的宽
      var w = document.documentElement.clientWidth;
      // 如果宽度大于1400px
      if (w > 1400) {
        // 侧边栏宽度为260px
        J_menu.style.width = "260px";
      }
      // 如果宽度小于1400px
      if (w < 1400) {
        for (var i = 0; i < len; i++) {
          // 给每个menuTitles的父元素宽度修改为40px
          menuTitles[i].parentNode.style.height = "40px";

          menuTitles[i].classList.remove("menu-list-title-active");
          J_menu.style.width = "75px";
          // 将当前属性值show修改为hidden
          menuTitles[i].flag = "hidden";
        }
      }
    });
    var btn = document.getElementById("button");
    // console.log(btn);
    btn.onclick = function () {
      var w = J_menu.clientWidth;
      // console.log(w);
      if (w < 100) {
        // 开,J_menu宽度变为260px
        J_menu.style.width = "260px";
      } else {
        // 关
        J_menu.style.width = "75px";
        for (var i = 0; i < len; i++) {
          // 属性值为show,给当前menuTitles删除menu-list-title-active类名
          menuTitles[i].classList.remove("menu-list-title-active");
          // 父元素高度修改为40px
          menuTitles[i].parentNode.style.height = "40px";
          menuTitles[i].flag = "hidden";
        }
      }
    };
```

## echar使用方法

1. 引入刚刚下载的 ECharts 文件
2. 为 ECharts 准备一个 DOM元素
3. 基于准备好的dom，初始化echarts实例
4. 指定图表的配置项和数据
5. 使用刚指定的配置项和数据显示图表。
