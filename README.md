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

// Template function accept rvalue reference parameter
template<typename T>
void fooTRV(const T&& v) // Important: "const" signs that it is rvalue only
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

fooTRV - обявление шаблонной функции принимающей rvalue ссылку. Обратить
внимание на **const** перед T&&; без него получится обявление функции
принимающей "Универсальную ссылку".

fooUR - это шаблонная функция принимающая "Универмальную ссылку" (Scott Meyers).
Т.е. функция может принимть как rvalue так и non-const-lvalue ссылки.
Для правильной передачи параметра v в качестве rvalue куда-то еще
необходимо использовать std::forward.

