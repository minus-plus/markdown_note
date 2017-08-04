## How to deal with inheritence of javascript
function Parent() {
	//
}
// add the properites that want to be interited to Paprent.prototype
function Child() {
	//
}

Child.prototype  = Object.create(parent.prototype);

Child.prototype.constructor = Child;

Child.prototype.__proto__ === Parent.prototype; // true


----
![prototype vs __proto__](https://i.stack.imgur.com/AGfN3.png)   
__proto__ and prototype has difference meanings. 
简单的来说，prototype目的是为了继承。将希望被继承的方法放到prototype上，这些方法就可以被继承。  
__proto__是为了property look up，__proto__依次将object本身和祖先类串联在一起，这样就能通过原型链look up祖先类的property。  
![](http://4.bp.blogspot.com/-ZaGWJf5fHcU/UGs_P61HOGI/AAAAAAAAAew/Kzl96APzqlk/s1600/Javascript+Prototypal+Inheritance+Diagram+-+grand+picture+-+with+some+Dog+objects+(1).png)   

var oo = Object.create(o);  
// oo.__proto__ === o, true  
Object.create will bind o.__proto__ to oo. 因此Object.create的主要作用是建立原型链。  
```
var o = {a:1, f: function(){}};
var oo = Object.create(o);
console.log(oo); //Object {}
console.log(oo.a) // 1
console.log(oo.f) //function (){}
```
#### new keyword
```
function Car() {
  this.name = "carName";
  this.modle = "carModel";
}

Car.prototype.move = function() {
  console.log("car is moving");
}
var car0 = new Car(); // equivalent to 
var car = {}; // (1)
Car.apply(car, []); // (2)
car.__proto__ = Object.create(Car.prototype); // (3)

```
