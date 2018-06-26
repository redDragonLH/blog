# 页面上copy 代码段 的实现
最近工作需要实现一个在页面里 copy 代码段功能，虽然是找了一个插件实现的，但是这个功能没做过，看了一下插件源码，找了下资料，总结一个文章，总归算是自己的知识了

以前只能借助falsh ，现在推出了关于 clipboard 的草案。  

- document.execCommand()
- ClipboardEvent

## execCommand()
 `document.execCommand('copy')` 只能 copy 可编辑区域内选中的内容，所以使用这个API ，就要有两个步骤
 
- 选中(select)
- 复制（copy）

而代码段显然不是可编辑区域，所以就必须多加一个步骤

- code 节点内的代码转移到一个 新建的 `textarea `里面
- 选中(select)
- 复制（copy）

      function copyCode(event) {
          event.preventDefault();

          var el = document.getElementById('copyCode'); 
          if (!el) { // 如果没有就创建一个用于放置内容等待copy的可编辑DOM
              el = document.createElement("textarea");
              el.style.position = "absolute";
              el.style.left = "-9999px";
              el.style.top = "0";
              el.id = 'copyCode';
              document.body.appendChild(el);
          }
          el.textContent = event.currentTarget.innerText;
          el.select(); // 选中内容

          document.execCommand('copy'); // 拷贝当前选中内容到剪贴板

      }

`el.select()` 方法用于选取文本域中的内容。

`document.execCommand('copy')` 用于触发`copy`事件，从可编辑区域获取内容

并且使用的是 `innerText` 去掉了多余的标签（刚开始我构想是在 代码高亮插件运行之前获取内容）

## clipboard 

*待续*