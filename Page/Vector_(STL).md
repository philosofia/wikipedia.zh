> 本文内容由[Vector \(STL\)](https://zh.wikipedia.org/wiki/Vector_\(STL\))转换而来。


**Vector** 是[C++標準程式庫中的一個](https://zh.wikipedia.org/wiki/C++標準程式庫 "wikilink")[類](../Page/类_\(计算机科学\).md "wikilink")，可視為會自動擴展容量的陣列，以循序(Sequential)的方式維護變數集合。vector的特色有支持隨機存取，在集合尾端增刪元素很快，但是在集合中間增刪元素比較費時。vector是[C++標準程式庫中的眾多](https://zh.wikipedia.org/wiki/C++標準程式庫 "wikilink")[容器](https://zh.wikipedia.org/wiki/容器_\(資料類型\) "wikilink")（*container*）之一。 vector以[模板](../Page/模板_\(C++\).md "wikilink")(泛型)方式實現，可以保存任意類型的變數，包括使用者自定義的資料型態，例如：它可以是放置整數（int）型態的 vector、也可以是放置字串（string）型態的 vector、或者放置使用者自定類別（user-defined class）的 vector。

## 設計

vector 定義於 <vector> 標頭檔中。與其他STL元件一樣，vector 屬於std名稱空間。

vector是[C++標準程式庫裡最基本的容器](https://zh.wikipedia.org/wiki/C++標準程式庫 "wikilink")，大多數狀況下都很有效率。vector設計之初即是為了改善C語言原生陣列的種種缺失與不便，而欲提供一種更有效、更安全的陣列。vector的使用介面刻意模擬C語言原生[陣列](https://zh.wikipedia.org/wiki/陣列 "wikilink")，較明顯的差異在於記憶體管理，原生陣列必須在宣告陣列的時候明確指定陣列長度(例如 int a\[5\])，但是 vector 不需要指定，而是會在執行期依據狀況自我調整長度，動態增大容量。

vector的表現一如[資料結構中的](https://zh.wikipedia.org/wiki/資料結構 "wikilink")[陣列](https://zh.wikipedia.org/wiki/陣列 "wikilink")，允許隨機存取(Random Access)，以索引值(index)存取任一元素只要花費常數時間 O(1)，在集合尾端增加或刪除元素也是花費常數時間O(1)，若在vector集合中間增加或刪除元素時間複雜度是線性時間O(n)，較為費時。雖然C++標準並沒有規定實作方式，但大多數 vector 內部均使用動態陣列方式實作。

### 成員函式概觀

`vector` 類別是以[容器（Container）](https://zh.wikipedia.org/wiki/容器_\(抽象数据类型\) "wikilink") 模式為基準設計的，也就是說，基本上它有 `begin()`，`end()`，`size()`，`max_size()`，`empty()` 以及 `swap()` 這幾個方法。

  - 存取元素的方法
      - `vec[i]` - 存取索引值為 i 的元素參照。 (索引值從零起算，故第一個元素是vec\[0\]。)
      - `vec.at(i)` - 存取索引值為 i 的元素的參照，以 at() 存取會做陣列邊界檢查，如果存取越界將會拋出一個例外，這是與operator\[\]的唯一差異。
      - `vec.front()` - 回傳 vector 第一個元素的參照。
      - `vec.back()` - 回傳 vector 最尾端元素的參照。
  - 新增或移除元素的方法
      - `vec.push_back()` - 新增元素至 vector 的尾端，必要時會進行記憶體配置。
      - `vec.pop_back()` - 刪除 vector 最尾端的元素。
      - `vec.insert()` - 插入一個或多個元素至 vector 內的任意位置。
      - `vec.erase()` - 刪除 vector 中一個或多個元素。
      - `vec.clear()` - 清空所有元素。
  - 取得長度/容量
      - `vec.size()` - 取得 vector 目前持有的元素個數。
      - `vec.empty()` - 如果 vector 內部為空，則傳回 true 值。
      - `vec.capacity()` - 取得 vector 目前可容納的最大元素個數。這個方法與記憶體的配置有關，它通常只會增加，不會因為元素被刪減而隨之減少。
  - 重新配置／重設長度
      - `vec.reserve()` - 如有必要，可改變 vector 的容量大小（配置更多的記憶體）。在眾多的 STL 實例，容量只能增加，不可以減少。
      - `vec.resize()` - 改變 vector 目前持有的元素個數。
  - 迭代 (Iterator)
      - `vec.begin()` - 回傳一個Iterator，它指向 vector 第一個元素。
      - `vec.end()` - 回傳一個Iterator，它指向 vector 最尾端元素的下一個位置（請注意：它不是最末元素）。
      - `vec.rbegin()` - 回傳一個反向Iterator，它指向 vector 最尾端元素的。
      - `vec.rend()` - 回傳一個Iterator，它指向 vector 的第一個元素的前一個位置。

## 使用說明

### 声明

使用 vector 之前，必須先 \#include<vector>。

声明一個 vector 變數的方法如下:

``` cpp
std::vector<T> v;
```

T 是 vector 要儲存的物件集合的型別，該 vector 的變數名稱是 v。T 可以是任何符合 Copy/Move Assignable 條件的型別，包括使用者自訂型別。如果 T 不符合 Copy / Move Assignable 或者複製 / 移动成本很高昂，可以考慮使用 T\* 甚至 std::unique_ptr<T> 來代替 T。

### 取代陣列使用

``` cpp
#include <vector>
#include <iostream>
int main() {
    std::vector<int> v;

    v.push_back(1);
    v.push_back(2);
    v.push_back(3);

    for(int i=0;i<3;++i)
        std::cout << v[i] << std::endl;
    system("pause");
    return 0;
}
```

### 長度/容量

[Vector_size_000.png](https://zh.wikipedia.org/wiki/File:Vector_size_000.png "fig:Vector_size_000.png") 以下程式碼是用來說明 vector 的長度變化。

``` cpp
//Headers and Macros
#include <iostream>
#include <cstdlib>
#include <vector>
#include <iomanip>
#define SETW_1 10
#define SETW_2 6
#define SETW_3 10

using namespace std;

typedef vector<int> Vint;

//利用參照取得真正的 capacity 值
void PrintVectorInfo(Vint& v)
{
    cout<<setw(SETW_1)<<"Element"<<setw(SETW_2)<<"Size";
    cout<<setw(SETW_3)<<"Capacity"<<endl;
    for ( Vint::iterator it = v.begin(); it != v.end(); it ++)
    {
        cout<<setw(SETW_1)<<(*it)<<setw(SETW_2)<<v.size();
        cout<<setw(SETW_3)<<v.capacity()<<endl;
    }
    cout<<endl;
}

//Main Function
int main(int argc, char** argv)
{
    //==START==//
    //宣告一個 vector
    Vint vint;
    //宣告兩個整數變數
    int a = 11, b = 22, c = 33;
    //建立只有一個元素空間的 vint
    //把變數 a 複製至第一個元素內
    vint.push_back(a);
    cout<<"Push Back: a = "<<a<<endl;
    //建立兩個元素空間的 vint
    //把變數 a 複製至第一個元素內
    //把變數 b 複製至第二個元素內
    //刪除上一次建立的 vint
    //上一次建立的 vint 只有一個元素空間
    //依此類推
    vint.push_back(b);
    cout<<"Push Back: b = "<<b<<endl;
    vint.push_back(c);
    cout<<"Push Back: c = "<<c<<endl;
    PrintVectorInfo(vint);
    //移除最後一個元素
    vint.pop_back();
    cout<<"Pop Back......"<<endl;
    PrintVectorInfo(vint);
    //移除最後一個元素
    vint.pop_back();
    cout<<"Pop Back......"<<endl;
    PrintVectorInfo(vint);
    //清除所有元素
    vint.clear();
    cout<<"Clear All Elements."<<endl;
    //==END==//
    system("pause");
    return 0;
}
```

### string 类型 Vector的使用

第一种：使用迭代器进行遍历

``` cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;
int main()
{
    vector<string> v(3, "I Love Wikipedia "); // 元素个数，每个元素的值相同
    for (vector<string>::const_iterator it = v.begin(); it < v.end(); ++it) // 输出Vector元素
        cout << *it << endl;
    system("pause");
    return 0;
}
```

输出结果为：

I Love Wikipedia

I Love Wikipedia

I Love Wikipedia

第二种，与int类型相同

``` cpp
#include<string>
#include <vector>
#include <iostream>
using namespace std;

int main()
{
    vector<string> vec;
    string str;
    str = "I Love WikiPedia";
    vec.push_back(str);
    vec.push_back("123");
    for(int i = 0; i < vec.size() ; ++i)
    {
        cout << vec[i] << endl;
    }
    system("pause");
    return 0;
}
```

输出结果为： I Love Wikipedia 123

## 優缺點探討

## 外部链接

  - [SGI 的 vector 使用說明（SGI STL specification of vector）](http://www.sgi.com/tech/stl/Vector.html)

  - [C++ 參考：vector（C++ reference: vector）](http://www.cplusplus.com/reference/stl/vector/)

  - [C++ 標頭檔說明（C++ Header description）](https://web.archive.org/web/20070927030825/http://www.roguewave.com/support/docs/sourcepro/edition9-update1/html/stdlibref/vector.html)

[Category:C++標準函式庫](https://zh.wikipedia.org/wiki/Category:C++標準函式庫 "wikilink") [Category:带有C++代码示例的条目](https://zh.wikipedia.org/wiki/Category:带有C++代码示例的条目 "wikilink")