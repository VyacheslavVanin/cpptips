# cpptips
my cpp tips on cxx11/14/and so on...

## Rvalue references
### Rvalue ссылка
```
class bar{
    ...
};

// Function accept usual rvalue reference parameter
void fooRV(bar&& b)
{
    ...
    lastFunc(std::move(v));
}

// Template function accept only rvalue reference parameter
template<typename T,
         typename = typename std::enable_if<std::is_rvalue_reference<T&&>::value>::type
        >
void fooTRV(T&& v)
{
    ...
    lastFunc(std::move(v));
}

// "Universal reference"
tempalte<typename T>
void fooUR(T&& v)
{
     ...
     lastFunc(std::forward<T>(v));
}
```
fooRV - обявление функции принимающей rvalue ссылку на класс bar.

fooTRV - обявление шаблонной функции принимающей rvalue ссылку.

fooUR - это шаблонная функция принимающая "Универсальную ссылку" (Scott Meyers).
Т.е. функция может принимть как rvalue так и non-const-lvalue ссылки.
Для правильной передачи параметра v в качестве rvalue куда-то еще
необходимо использовать std::forward.

### Перемещаемый объект

Для того чтобы объект мог быть перемещен необходимо выполнение одного из
условий:
- Класс объекта не должен содержать ни одного метода из "Big five":
    - деструктора
    - конструктура копирования
    - оператора копирующего присваивания
    - контруктора перемещения
    - оператора перемещающего присваивания
- Класс должен содержать все методы из "Big five", при этом конструктор
перемещения, и оператор перемещающего копирования должны быть **noexcept**

## Variadic templates

### Example
```
template<typename... Args>
void f_by_values(Args... args)
{
    ...
    foo(args...);
}

template<typename... Args>
void f_by_const_refs(const Args&... args)
{
    ...
    foo(args...);
}

template<typename... Args>
void f_by_universal_ref(Args&&... args)
{
    ...
    foo(std::forward<Args>(args)...));
}
```
f_by_values - аналогично передаче всех параметров по значению.
f_by_const_refs - аналогично передаче всех параметров по константным ссылкам.
f_by_universal_ref - передача всех параметров по "унивесальным ссылкам", также пример "Perfect forwarding".
