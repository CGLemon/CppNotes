# Key Word: Explicit

在 C++ 裡會有一些隱式轉換，增加方便性

```cpp
class MyInt {
public:
    MyInt(int a) {
        a_ = a;
    }

    operator char() { return a_; }

private:
    int a_;    
};

int main() {
    MyInt i = 10; // 對 10 做 copy initialization，選擇構造函數 MyInt(int a)
    char c = i; // 轉換成 char c = char(i)

    return 0;
}
```

但是 C++ 的整體的建構函數非常複雜，實際上我們很難完全掌握編譯器的行為 ，加入 explicit 關鍵詞可以避免任何潛在的 implicit conversions 和 copy initialization，


```cpp
class MyInt {
public:
    explicit MyInt(int a) {
        a_ = a;
    }

    explicit operator char() { return a_; }

private:
    int a_;    
};

int main() {
    MyInt i = 10; // 錯誤，對 10 做 copy initialization 被禁止
    char c = i; // 錯誤，對 operator 的 conversions 被禁止

    return 0;
}
```
