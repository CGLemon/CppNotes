# struct V.S. class

struct 是從 C 語言保留下來的關鍵詞，經過多次 C++ 表準擴充，struct 和 class 的界面基本相差無幾，但它們還是有一些區別

### 成員

class 的成員預設為 private，而 struct 預設為 public。

### 記憶體

struct 保證記憶體的排列和宣告的順序相同，而 class 不保證。
