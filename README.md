# cpptips
my cpp tips on cxx11/14/and so on...

## Rvalue references
```
tempalte<typename T>
void foo(T&& v)
{
     ...
     lastFunc(std::forward<T>(v));
}
```
Это шаблонная функция принимающая "Универмальную ссылку" (Scott Meyers). Т.е. функция может принимть как rvalue так и non-const-lvalue ссылки. Для правильной передачи параметра v в качестве rvalue куда-то еще необходимо использовать std::forward.

