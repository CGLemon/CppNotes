# Perfect Forwarding（完美轉發）

## Forwarding references

C++ 函數模板有自動推論的能力，如果同一個函數有多個 overload ，它可以根據類別決定使用那一個。

```cpp=
#include <iostream>

template<typename T>
void func(T&& a) {
    printf("passed by rval\n");
}

template<typename T>
void func(T& a) {
    printf("passed by lval\n");
}

int main(int argc, char **argv) {

    int a = 0;
    func(0); // passed by rval
    func(a); // passed by lval

    return 0;
}
```

我們也可以使用 [Forwarding References](https://en.cppreference.com/w/cpp/language/reference#Forwarding_references) 方法，將多個函數合併成一個函數，Forwarding References 是一種特殊的值分類方式，在 cv-unqualified 的函數模板右值中，可以根據傳遞參數的左右值傳決定類別。

```cpp=
#include <iostream>

template<typename T>
void func(T&& a) {}

int main(int argc, char **argv) {

    int a = 0;
    func(0); // 函數解析為 func<int&&>(int&&)
    func(a); // 函數解析為 func<int&>(int&)

    return 0;
}
```

## Perfect Forwarding

一般的 Forwarding 有一個問題，編譯器會因為效率，自行決定使用那一個函數或模板的型態，例如下方，宣告了一個右值 ```a``` ，但卻是通過左值傳送給函數。間單來講，一般的 Forwarding 可能會有非預期型態轉換。

```cpp=
#include <iostream>

template<typename T>
void func(T&& a) {
    printf("passed by rval\n");
}

template<typename T>
void func(T& a) {
    printf("passed by lval\n");
}

int main(int argc, char **argv) {

    int &&a = 0;
    func(a); // passed by lval

    return 0;
}
```

Perfect Forwarding 可以避免這個問題，使用函數 ```std::forward<T>(T arg)``` ，可以看到呼叫預期的函數。

```cpp=
#include <iostream>
#include <utility>

template<typename T>
void func(T&& a) { 
    printf("passed by rval\n");
}

template<typename T>
void func(T& a) {
    printf("passed by lval\n");
}

int main(int argc, char **argv) {

    int &&a = 0;
    func(std::forward<int&&>(a)); // passed by rval

    return 0;
}
```

Perfect Forwarding 最大作用就是和 Forwarding References 一起使用，如果不使用 Perfect Forwarding，那麼 ```wrapper``` 無論如何都會呼叫 ```func(T& a)``` ，但使用後，它可以呼叫預期的函數。

```cpp=
#include <iostream>
#include <utility>

template<typename T>
void func(T&& a) { 
    printf("passed by rval\n");
}

template<typename T>
void func(T& a) {
    printf("passed by lval\n");
}

template<typename T>
void wrapper(T&& arg) {
    func(std::forward<T>(arg));
}

int main(int argc, char **argv) {

    int a = 0;
    func(0); // passed by rval
    func(a); // passed by lval

    return 0;
}
```
