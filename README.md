# javascript-Singleton-Pattern
javascript单例模式介绍
<h3>维基百科单例模式介绍</h3>
单例模式，也叫单子模式，是一种常用的软件设计模式。在应用这个模式时，单例对象的类必须保证只有一个实例存在。许多时候整个系统只需要拥有一个的全局对象，这样有利于我们协调系统整体的行为。比如在某个服务器程序中，该服务器的配置信息存放在一个文件中，这些配置数据由一个单例对象统一读取，然后服务进程中的其他对象再通过这个单例对象获取这些配置信息。这种方式简化了在复杂环境下的配置管理。

实现单例模式的思路是：一个类能返回对象一个引用(永远是同一个)和一个获得该实例的方法（必须是静态方法，通常使用getInstance这个名称）；当我们调用这个方法时，如果类持有的引用不为空就返回这个引用，如果类保持的引用为空就创建该类的实例并将实例的引用赋予该类保持的引用；同时我们还将该类的构造函数定义为私有方法，这样其他处的代码就无法通过调用该类的构造函数来实例化该类的对象，只有通过该类提供的静态方法来得到该类的唯一实例。

单例模式在多线程的应用场合下必须小心使用。如果当唯一实例尚未创建时，有两个线程同时调用创建方法，那么它们同时没有检测到唯一实例的存在，从而同时各自创建了一个实例，这样就有两个实例被构造出来，从而违反了单例模式中实例唯一的原则。 解决这个问题的办法是为指示类是否已经实例化的变量提供一个互斥锁(虽然这样会降低效率)。

<h3>一个简单的小栗子</h3>
```html
<!DOCTYPE html>
<html>
<head>
<title>singleleton</title>
</head>
<body>
<button type="button" id="loginBtn">登陆</button>
<script>
//创建我们的方法，方法为一个自调用匿名函数（作用类似闭包）
var createLoginLayer=(function(){
     //在闭包内部声明一个实例（就是一对象）用来存储一个单例实例的引用,意思就是当外部引用 createLoginLayer方法时，实际上应用的就是下面声明的这个对象
     var div ;//初次运行div为空，转换成布尔值是false
     if(!div){//初次运行为true，创建实例的引用
        div=document.createElement('div);
        div.innerHTML='hello world';
        div.style.display='none';
        document.body.appendChild(div);
     }
     return div;//创建的实例引用要返回
})();
var loginBtn=document,getElementById("loginBtn");
loginBtn.onclick=function(){
   //注意！！要调用方法了
   var loginLayer = createLoginLayer();
   loginLayer.style.display = 'block';
}
</script>
</body>
</html>
```
