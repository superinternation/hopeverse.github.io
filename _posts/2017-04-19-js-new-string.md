---
layout: post
title: "对javascript中string()对象中常见以及偏冷门方法进行的梳理"
author: "hopeverse"
---
 

记录js中string()对象中的一些常见的，或者是稍微难以分辨的方法

<br/>

### CharAt()方法

>返回指定位置字符串，括号内参数为需要返回第几位的字符串

```
<script>
    var rec = "hello world!";
    alert(rec.charAt(2));
</script>

```


### indexOf()方法

>检索字符串，返回某个字符串首次出现的位置

```
<script>
    var rec = "hello world!";
    alert(rec.indexOf("o"));
    //弹出4.  这是第一个o出现的位置 
    alert(rec.indexOf("o",rec.indexOf("o")+1));
    //弹出7.  这是第二个o出现的位置，还是检索o，然后开始位置为第一个o加1的位置进行检索
</script>

```


### match()方法

>在字符串中查找指定的值，并返回。

```
    <script>
        var rec = "hello world!";
        alert(rec.match("world!"));
        //弹出world！
    </script>

```


### replace()方法

>用一段字符串替换另一端字符串，或者替换一段与正则表达式匹配的子串

```
     <script>
        var rec = "hello world!";
        alert(rec.replace(/world!/,"china"));
        //弹出hello china! 
        // 注意！ 需要替换的字符串用双斜线包括,新字符串用双引号包含
    </script>

```


### split()方法

>把字符串分割成字符串数组
>第一个参数：是以什么作为标准进行分割  例如 "，" " ",""或者说字符串中的某个符号。
>第二个参数：返回数组的长度，如果是3，那么超过3段的都不会显示

```
        <script>
            var rec = "hello world!";
            alert(rec.split(" ",1));
            //弹出hello 
            // 这里以空格为分割标准，截取1个字符串数组。就算分割出来有hello和world两个字符串数组，但是控制了只截取一个，那么返回的也就只有一个。
        </script>

```


### slice()方法

>第一个参数: 要抽取的字符串开始位置，下标正数从左往右，下表为负数从尾部往前算。
>第二个参数：抽取字符串结尾的下标(不包含下标，下标-1的字符串)。如果此参数没有设置，那么从开始位置，一直截取到末尾的字符串，如果为负数，那么从末尾往前算的位置

```
        <script>
            var rec = "hello world!";
            alert(rec.slice(0,5));
            //弹出hello
            // 这里开始为0的下标，结束为5.那么不会包含第五个字符串，需要-1才是结束的位置。
        </script>
-------------------------------------------------------------------------------------
       
        <script>
            var rec = "hello world!";
            alert(rec.slice(6));
            //弹出world！
            // 这里开始为6,没有设置结束的下标位置.那么就是一直截取到最后.
        </script>
-------------------------------------------------------------------------------------
        <script>
            var rec = "hello world!";
            alert(rec.slice(0,-7));
            //弹出hello
            // 这里开始为0,结束下标为-6,那么从后往前算第6位.
        </script>


```

### substr()方法

>第一个参数：必需而且是数值，如果是负数那么从末尾往前算，-1为倒数第一个，以此类推
>第二个参数：这里也必须是数值，那么表示截取多长的字符串

```
        <script>
            var rec="hello world!"
            alert(rec.substr(3,7))
            //弹出lo worl  7是截取的字符串长度，所以索引不从0开始
        </script>

```


### substring()方法

>第一个参数：非负整数，第一个字符开始的位置
>第二个参数：非负整数，结束的位置-1 
>所以此方法返回值是：第一个参数的索引，和第二个参数的索引-1之间的字符串

```
        <script type="text/javascript">
            var rec="hello world!"
            alert(rec.substring(3,7))
        </script>
```


### concat()方法

>用于连接两个或者多个字符串

```
        <script>
            var rec1="hello ";
            var rec2="world";
            alert(rec1.concat(rec2));
            //弹出hello world ，其中rec1后面要加了个空字符，不然两个字符串连接在一起非常紧密
        </script>

```


### toUpperCase()方法

>把字符串中所有的小写字母转换成大写字母

```
        <script>
            var rec="hello world!"
            alert(rec.toUpperCase());
            //弹出HELLO WORLD!
        </script>

```


### toLowerCase()方法

>把字符串中所有的大写字母转换成小写字母

```
        <script>
            var rec="HELLO WORLD!"
            alert(rec.toLowerCase());
            //弹出hello world！
        </script>

```

### search()方法

>搜索字符串，需要搜索的字符用//包括起来，对大小写敏感，如果没有对应的字符，那么返回-1，如果搜索的到，那么返回的数字则是从被搜索的字符，之前所有的length,其中包括空字符

```
        <script>
            var rec="sss W3School!"
            alert(rec.search(/W3Sc/));
            //弹出4   弹出内容为从字符串开始，到刚好被搜索到字符的前一位的length
        </script>

```


### font()方法

>按规定的字体设置显示字符串

```
        <script>
            var rec="hello world！";
            document.write(rec.fontcolor("red"));
            //这里字体设置成了红色，同样，改成fontsize也是可行的。
        </script>

```


>到这里，关于string对象的一些方法已经记录完成了，梳理了一下，这一些方法其中有一些比较冷门，也有不乏让人经常分不太清除的方法，需要好好的理解了。记录的比较粗略，其中有一部分方法也可以在正则表达式中使用，需要更加详细的请自行Google.如需转载，请注明出处

[https://liutianzhu.me](https://liutianzhu.me)