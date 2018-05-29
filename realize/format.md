# format

看插件源码的时候看到一个貌似很厉害的模板替换方法，记录下来学习

      function format (format, args) {
          return format.replace(/\{(\d+)\}/g, function(m, n){
              return args[n] ? args[n] : m;
          });
      }

把需要替换的内容 写成 `{\d}` (里面是数字) 的样式,把需要替换的字符串和用于替换的内容传入到方法里面