# Operator overloading

**overload** 代表重新定義該符號的功能。

## [影片](https://youtu.be/fIEkpbGiOLI)

## 以"加號"為例 

舉例來說:
```cpp
#include<iostream>

class Box {
public:
    Box(double l,double b,double h):length(l),breadth(b),height(h){};
    Box():length(0),breadth(0),height(0){};    
private:
    double length;      // Length of a box
    double breadth;     // Breadth of a box
    double height;      // Height of a box
};
int main(){
    Box box1(5,5,5);
    Box box2(1,1,1);
    Box box3 = box1+box2;
}
```

![](https://i.imgur.com/aTvg6Lc.png)

編譯器會報錯，不能夠直接把個 **box1** 和 **box2** 加起來。需要 **overload operator** $!$

```cpp
#include<iostream>

class Box {
public:
    Box(double l,double b,double h):length(l),breadth(b),height(h){};
    Box():length(0),breadth(0),height(0){};  
    
    // Overload + operator to add two Box objects.
    Box operator+(const Box& b) {
        Box box;
        box.length = this->length + b.length;
        box.breadth = this->breadth + b.breadth;
        box.height = this->height + b.height;
        return box;
    }
	
private:
    double length;      // Length of a box
    double breadth;     // Breadth of a box
    double height;      // Height of a box
};
int main(){
    Box box1(5,5,5);
    Box box2(1,1,1);
    Box box3 = box1+box2;
}
```

## 以"大於"、"小於"符號為例
```cpp
#include<iostream>

class Box {
public:
    Box(double l,double b,double h):length(l),breadth(b),height(h){};
    Box():length(0),breadth(0),height(0){};  	
private:
    double length;      // Length of a box
    double breadth;     // Breadth of a box
    double height;      // Height of a box
};
int main(){
    Box Box1(5,5,5);
    Box Box2(1,1,1);
    if(Box1 > Box2){
		std::cout << "Box1 > Box2" << std::endl;
	}
	
    Box Box3(3,3,3);
    Box Box4(10,10,10);
    
    if(Box3 < Box4){
        std::cout << "Box3 < Box4" << std::endl;
    }
}
```

![](https://i.imgur.com/pjZlXYb.png)


這邊我定義 
* **A > B** 代表 **A** 的 **length,breadth,height** 都大於 **B**
* **A < B** 代表 **A** 的 **length,breadth,height** 都小於 **B**

```cpp
#include<iostream>

class Box {
public:
    Box(double l,double b,double h):length(l),breadth(b),height(h){};
    Box():length(0),breadth(0),height(0){};  
    
    // Overload > operator 
    bool operator>(const Box &b){
        return (this->length > b.length) && (this->breadth > b.breadth) && (this->height > b.height);
    }

    // Overload < operator 
    bool operator<(const Box &b){
        return (this->length < b.length) && (this->breadth < b.breadth) && (this->height < b.height);
    }
	
private:
    double length;      // Length of a box
    double breadth;     // Breadth of a box
    double height;      // Height of a box
};
int main(){
    Box Box1(5,5,5);
    Box Box2(1,1,1);
    if(Box1 > Box2){
		std::cout << "Box1 > Box2" << std::endl;
	}
	
    Box Box3(3,3,3);
    Box Box4(10,10,10);
    
    if(Box3 < Box4){
        std::cout << "Box3 < Box4" << std::endl;
    }
}
```