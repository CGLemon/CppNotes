# Conversions

## Conversion Rank

Conversion Rank 依序 bool, char, short, int, long, long long 排列，越右邊 rank 越大。Conversion Rank 不分有號數和無號數，例如，unsigned char 和 char 的 conversion rank 一樣大

## Conversion Rule

在預設的情況下，轉換的順序依照 1 到 5 執行，但如果某一條轉換成立，則結束執行。

1. 如果其中一個算子是定義在 enum 內的，則不轉換。
2. 如果其中一個算子的型態是 ```lone double``` ，則另一個算子轉換成 ```lone double``` 。
3. 如果其中一個算子的型態是 ```double``` ，則另一個算子轉換成 ```double``` 。
4. 如果其中一個算子的型態是 ```float``` ，則另一個算子轉換成 ```float``` 。
5. 如果兩個算子皆為整數型態（包括 ```bool``` 型態），則有以下可能：
   * 如果兩個算子同為無號數或是有號數，則同時轉換成兩個型態中，最大的 conversion rank 的型態。
   * 不然，如果無號數的 conversion rank 大於等於另一個有號數，則有號數轉換成無號數的型態。
   * 不然，如果有號數可以表示所有無號數的值，則無號數轉換成有號數的型態。
   * 不然，都轉換成對應的無號數相加。
