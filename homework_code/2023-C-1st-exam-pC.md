
# 階段考第3題

## 題目連結
https://neoj.sprout.tw/problem/594/

## 出題者給大家的話
純粹的實作題目 **，** 無論是手刻 strcat、strcpy 或利用 C/C++ library中寫好的函式都可以解出來 **!** 

這題預設大家使用 c style string 解題，下面的講解也會用c style string function 來解題 **!**

> std::string是二階才會教的東西。

## 題目觀察

```cpp
< In testcase3 > 

Original message : Ihaveaappleandpineapple
計次 count=0
-----------------------------------------------------------------------------
| errors |      dirty message       |            description                |
----------------------------------------------------------------------------|
|  a     | Ih-ve--pple-ndpine-pple  | There are five "a" in the message     |
|  apple | Ih-ve--pple-ndpine-pple  | There are zero "apple" in the message |
|  pple  | Ih-ve-------ndpine-----  | There are two  "pple" in the message  |
-----------------------------------------------------------------------------
Destroyed messages a total of 7 times.
```

可見:
> 每個 **error** 都會對 **original** **message** 遍歷一次。若是掃描到 **original** **message** 中含有 **error** ， **count**就會 **+1**。

如上圖的範例:
> * **error** 為 **a** 的時候，用 **a** 遍歷一遍 **message** ， 其在 **message** 中出現了 **5** 次。
> * **error** 為 **apple** 的時候，用 **apple** 遍歷一遍 **message** ， 其在 **message** 中出現了 **0** 次。
> * **error** 為 **pple** 的時候，用 **pple** 遍歷一遍 **message** ， 其在 **message** 中出現了 **2** 次。

## 解法

假設 **error** 長度為 **error** _ **length** ， **message** 長度為 **message** _ **length**

對於所有的 **i**，對 **message[i]** ~ **message[i+error** _ **length-1]** 做 **strcmp**。

$0\leq i \leq message$ _ $length-1$

* 若字串一樣，把 **message** 用 **"-"** 代換(如同題意的破壞)，並 **count**++
* 若字串不一樣，就只是 **i+1** 繼續比對。

其中請注意，**strcmp** 的範圍 可能會超過 **message** _ **length**，要寫個判斷式避免這類情況。

## AC code

### 竹區
```cpp
#include<iostream>
#include<cstring>
using namespace std;
int main(){

    int n;
    cin >> n;

    char error[100][1005];
    int error_length[100];
    for(int i=0;i<n;i++){
        cin >> error[i];    
        error_length[i] = strlen(error[i]);
    }
    
    char message[1005];
    cin >> message;
    
    int cnt=0;
    int message_length = strlen(message);
    for(int t = 0; t < n ; t++){
        for(int i = 0 ; i < message_length ; i++){
            char tmp[1005]={'\0'};
            strncpy(tmp,message+i,error_length[t]);
            if( (message_length-i) < error_length[t] ) continue;
            if(!strcmp(tmp,error[t])){
                cnt++;
                for(int j=0;j<error_length[t];j++){
                    *(message+i) = '-';
                }
            }
        }
    }
    cout << cnt << endl;
}
```
### 北區
```cpp
#include <iostream>
#include <cstring>

int main(){
    int n;
    char error[10][102];
    char message[1003];
    std::cin >> n;
    for (int i=0 ; i<n ; i++) std::cin >> error[i];
    std::cin >> message;
    int len[10];
    for (int i=0 ; i<n ; i++) len[i] = strlen(error[i]);
    int length = strlen(message), answer = 0;
    for (int i=0 ; i<length ; i++){
        for (int j=0 ; j<n ; j++){
            if (strncmp(error[j], message+i, len[j]) == 0){
                i += (len[j]-1);
                answer ++;
            }
        }
    }
    std::cout << answer << std::endl;
}
```