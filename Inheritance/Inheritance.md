// В ES2015 класс создается так:  
class MyClass {  
  constructor(value) {  
    this._field = value;  
  }  
  myMethod() {  
    return this._field;  
  }  
}

var obj = new MyClass(5);  
alert(obj.myMethod);

Тоже самое в ES5 будет так:  
function MyClass(value) {  
    this._field = value;  
}

MyClass.prototype.myMethod = function() {  
    return this._field;  
};

var obj = new MyClass(5);  
alert(obj.myMethod());

В ЕС2015 наследование выглядит так:  
class OtherClass extends MyClass {  
    constructor(value) {  
        super(value*2);  
    }  
    myMethod() {  
        return super.myMethod()*2;  
    }  
}  

var obj = new OtherClass(10);  

obj instanceof MyClass; // true  
obj instanceof OtherClass; // true  

В ES5 с этим чуть сложнее:  
function OtherClass(value) {  
    MyClass.call(this, value);  
}  

OtherClass.prototype = Object.create(MyClass.prototype);  
OtherClass.prototype.constructor = OtherClass;  
OtherClass.prototype.myMethod = function() {  
    return MyClass.prototype.myMethod.call(this);  
};
