# this
javascript的this总是指向一个对象，而具体指向哪个对象实在运行时基于函数的执行环境动态绑定的，而非函数被声明时的环境

实际应用中，this的指向大概分为以下四种

1.作为对象的方法调用

2.作为普通函数调用

3.构造器调用

4.Function.prototype.call或者Function.prototype.apply调用

1.作为对象的方法调用,this指向该对象

var obj={

a:1,
getA:function(){

console.debug(this===obj);//输出true

console.debug(this.a);//1

}

};

obj.getA();

2.作为普通函数调用当函数，这个全局对象是window对象

window.name='globalName';

var getName=function(){

  return this.name;
  
}

console.debug(getName());

或者

window.name='gloabalName';

var myObject={

    name:'seven',
    
    getName:function(){
    
    return this.name;
    
    }
    
};

var getName=myObject.getName;

console.debug(getName());

局部callback方法，用一个变量保存div节点的引用；

window.id='window';

document.getElementById('div1').onclick=function(){

console.debug(this.id);//输出div1

var callback=function(){

    console.debug(this.id);//输出window
    
}

callback();

};

解决方案为:用一个变量保存div节点的引用

window.id='window';

document.getElementById('div1').onclick=function(){

console.debug(this.id);//输出div1

var that=this;

var callback=function(){

    console.debug(that.id);//输出div1
    
}

callback();

};

3.构造函数跟普通函数一模一样，它们的区别在于被调用的方式

  当用new运算符调用函数的时候，该函数总会返回一个对象，通常情况下构造器里面的this就指返回的这个对象
  
  如代码 var MyClass=function(){
  
         this.name='seven';
         
         }
         
         var obj=new MyClass();
         
         console.debug(obj.name);//输出seven
         
  但是，
  
  使用new调用构造函数时，还要注意一个问题，如果构造器显式的返回了一个object类型的对象，那么此次运算结果最终会返回这个对象
  
      var MyClass=function(){
      
         this.name='seven';
         
         return{
         
              name:'anne'
              
         }
         
         };
         
         var obj=new MyClass();
         
         console.debug(obj.name);//输出anne
         
  如果构造器不显式地返回任何数据，或者是返回一个非对象类型的数据，就不会造成上述问题
  
      var MyClass=function(){
      
         this.name='seven';
         
         return 'anne'
         
         };
         var obj=new MyClass();
         
         console.debug(obj.name);//输出sve
         
4.Function.prototype.call和Function.prototype.apply可以动态地改变传入函数的this:


      var obj1={
      
          name:'sven',
          
          getName:function(){
          
             return this.name;
             
          }
      };
      var obj2={
      
          name:'anne'
          
      };
      console.log(obj1.getName());//输出sven;
      
      console.log(obj2.getName.call(obj2));//输出anne;
