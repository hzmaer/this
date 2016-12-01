# this
javascript的this总是指向一个对象，而具体指向哪个对象实在运行时基于函数的执行环境动态绑定的，而非函数被声明时的环境
实际应用中，this的指向大概分为以下四种
1.作为对象的方法调用
2.作为普通函数调用
3.构造器调用
4.Function.prototype.call或者Function.prototype.apply调用

1.作为对象的方法调用
var obj={
a:1,
getA:function(){
console.debug(this===obj);//输出true
console.debug(this.a);//1
}
};
obj.getA();

2.作为普通函数调用当函数
