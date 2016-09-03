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

