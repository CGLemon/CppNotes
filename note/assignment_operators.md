# Assignment Operators（指定運算子）

指定運算子是一種二元運算子，它可以重新指定左方算子的值。所有指定運算子都是從右至左結合，且左方算子必須是可修改左值（ modifiable lvalue ）。指定運算子的成員有 ```=```, ```*=``` , ```/=```, ```%=```, ```+=```, ```-=```, ```<<=```, ```>>=```, ```&=```, ```^=```, ```|=```。


## direct assignment（直接指定）

直接指定格式為

| Expressions            | Note                           |
| :--------------------: | :----------------------------: |
|   ```lhs = rhs```      |                                |
|   ```lhs = {}```       | braced-init-list, since C++11  |
|   ```lhs = {rhs}```    | braced-init-list, since C++11  |


其中 ```rhs``` 必須是能被隱式轉換（ implicitly convertible ）成可接受的型態。需要注意的是，定義並非是指定運算子，如下。

```cpp
int main(int argc, char **argv) {

    int a = 0; // not assignment
    a = 12     // assignment operator

    return 0;
}

```

## Compound Assignment（複合指定）

複合指定格式為

| Expressions            | Note                           |
| :--------------------: | :----------------------------: |
|   ```lhs op rhs```     |                                |
|   ```lhs op {}```      | braced-init-list, since C++11  |
|   ```lhs op {rhs}```   | braced-init-list, since C++11  |

其中 ```rhs``` 必須是能被隱式轉換（ implicitly convertible ）成可接受的型態。它的運算式 ```E1 op E2``` 可以被翻譯成 ```E1 = E1 op E2```，它們的行為等價。
