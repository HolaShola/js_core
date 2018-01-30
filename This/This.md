Значение this напрямую связанно с типом исполняемого кода контекста. Определяется оно при входе в контекст и на протяжении исполнения кода контекста, является неизменным.

                                        activeExecutionContext = {
                                            VO: {...},    // объект переменных (variable object)
                                            this: thisValue
                                        };


    THIS В ГЛОБАЛЬНОМ КОДЕ
Здесь довольно всё просто. В коде глобального контекста, значением this всегда является сам глобальный объект (global); таким образом, можно косвенно к нему обратиться:

                                        // явное объявление свойства глобального объекта
                                        this.a = 10; // global.a = 10
                                        alert(a); // 10
                                        
                                        // косвенное, посредством присваивания
                                        // неопределённому до этого идентификатору
                                        b = 20;
                                        alert(this.b); // 20
                                        
                                        // также косвенное, посредством объявления
                                        // переменной, поскольку объектом переменных
                                        // в глобальном контексте является сам глобальный объект
                                        var c = 30;
                                        alert(this.c); // 30    

    THIS В КОДЕ ФУНКЦИИ
В коде функции this не связано статично с функцией. this определяется при входе в контекст, и в случае с кодом функции, каждый раз может быть абсолютно разным.
При обычном вызове функции, this определяется вызывающей стороной, которая активирует код контекста функции, — так называемый, caller, т.е. родительский контекст, который вызывает функцию. Определение значения this происходит по форме выражения вызова (иными словами, как синтаксически вызвана функция).

Обычную глобальную функцию можно активировать разными формами вызова, которые и влияют на разное значение this:

                                        function foo() {
                                            alert(this);
                                        }
                                        
                                        foo(); // global
                                        
                                        alert(foo === foo.prototype.constructor); // true
                                        
                                        // но при иной форме вызова той же
                                        // функции, this будет иметь уже другое значение
                                        
                                        foo.prototype.constructor(); // foo.prototype

Аналогично можно вызвать функцию, описанную как метод объекта, но значением this не будет являться этот объект:

                                        var foo = {
                                        bar: function () {
                                            alert(this);
                                            alert(this === foo);
                                        }
                                        };
                                        
                                        foo.bar(); // foo, true
                                        
                                        var exampleFunc = foo.bar;
                                        
                                        alert(exampleFunc === foo.bar); // true
                                        
                                        // опять же, при иной форме вызова той же
                                        // функции, this уже установлен в другое значение
                                        
                                        exampleFunc(); // global, false
