^字符是指主版本中的最新版本 因此， ^0.4.0 是指版本号为 的最新版
本，当前为 0.4. 19
^字符除了提供的主版本号之外不针对任何其他主版本
• Solidity 文件只能用主版本号为 的编译器进行编译，不能在其他主版本
号的编译器上编译

## 版本和蛛丝
~~~ solidity
// 指定版本
pragma solidity 0.4.19;

// This is a single line comment in Solidity

/* This is a multi-line comment
     In solidity. Use this when multiple consecutive lines
Should be commented as a whole */
~~~

## import语句
语法`import 'filename';`

## 合约
关键字是严格区分大小写的
~~~solidity
pragma solidity 0.4.19;

// This is a single line comment in Solidity

/* This is a multi-line comment
     In solidity. Use this when multiple consecutive lines
Should be commented as a whole */

contract firstCOntract {
    
}

contract secondContract {
    
}

library stringLibrary {
    
}

library mathLibrary {
    
}

interface IBank{
    
}

interface IAccount {
    
}

~~~

### 合约的结构
状态变量
结构定义
修改器定义
事件声明
枚举定义
函数定义

例子：
~~~solidity

pragma solidity 0.4.19;

//contract definition
contract generalStructure {
    //state variables
    int public stateIntVariable; // vriable of integer type
    string stateStringVariable; //variable of string type
    address personIdentifier; // variable of address type
    myStruct human; // variable of structure type
    bool constant hasIncome = true; //variable of constant nature
    
    //structure definition
    struct myStruct {
        string name; //variable fo type string
        uint myAge; // variable of unsigned integer type
        bool isMarried; // variable of boolean type
        uint[] bankAccountsNumbers; // variable - dynamic array of unsigned integer
    }
    
    //modifier declaration
    modifier onlyBy(){
        if (msg.sender == personIdentifier) {
            _;
        }
    }
    
    // event declaration
    event ageRead(address, int );
    
    //enumeration declaration
    enum gender {male, female}
    
    //function definition
    function getAge (address _personIdentifier) onlyBy() payable external returns (uint) {
       
       human =  myStruct("Ritesh",10,true,new uint[](3)); //using struct myStruct
       
       gender _gender = gende的.male; //using enum 
       
       ageRead(personIdentifier, stateIntVariable);
    }
    
}
~~~

### 状态变量
状态变量是 Solidity 合约最重要的特性之一。状态变量由矿工永久存储在区块链/以太坊账本中。在合约中，没有在任何函数内声明的变量称为状态变量。状态变量存储合约的当前值。状态变量的内存是静态分配的，并且在合约生命周期内不能更改(分配的内存大小)。必须静态定义每个状态变量的类型Solidity 编译器必须确定每个状态变量的内存分配细节，因此必须声明状态变量的数据类型。

限定符：
- internal:默认情况下，如果没有指定任何内容，则状态变量具有internal限定符。这意味着这个变量只能在当前的合约函数和任何继承它们的合约中使用。这些变量不能被外部访问修改，但是，可以查看它们。内部状态变量的示例如下所示:
`int internal StateVariable;`
- private:这个限定符就像 internal 上附加的约束。私有状态变量只能在声明它们的合约中使用。即使在派生合约中也不能使用它们。私有状态变量的示例如下所示:
`int private privateStateVariable;`
- public:这个限定符使得状态变量可以直接访问。Solidity 编译器为每个公共状态变量生成一个 getter 函数。公共状态变量的示例如下:
`int internal stateIntVariable;`
- constant : 这个限定符使得状态变量不可变。变量声明时必须赋初值实际上，编译器会在所有代码中将变量的引用替换为指定的值。常量状态变量的示例如下:
`boolean constant hasIncome`

### 结构
~~~solidity

pragma solidity 0.4.19;

//contract definition
contract generalStructure {
    //state variables
    
    //structure definition
    struct myStruct {
        string name; //variable fo type string
        uint myAge; // variable of unsigned integer type
        bool isMarried; // variable of boolean type
        uint[] bankAccountsNumbers; // variable - dynamic array of unsigned integer
    }
    
    // state structure
    myStruct  stateStructure = myStruct("Ritesh", 10, true, new uint[](2));
    
    myStruct  stateStructure1;
    
    
    //function definition
    function getAge ()  returns (uint) {
    
       // local structure    
       myStruct memory localStructure = myStruct("Modi", 20 ,false, new uint[](2));
       
       //local pointer to State structure
       myStruct pointerStructure = stateStructure;
       
       // pointerlocalStructure is reference to localStructure
       myStruct memory pointerlocalStructure = localStructure;
       
       //changing value in localStructure
       localStructure.myAge = 30;
       
       //assigning values to state variable
       stateStructure1 =   myStruct("Ritesh", 10, true, new uint[](2));
       
       //returning pointerlocalStructure.Age -- returns 30
       return pointerlocalStructure.myAge;

    }
    
}

~~~

### 修改器
方法会被修改器所限制--修改器可以限制方法的行为，但是方法谁都可以调用，但只有满足了修改器行为才会生效
~~~solidity
    //modifier declaration 修饰符声明--修改器声明
    modifier onlyBy(){
        if (msg.sender == personIdentifier) {
            _;
        }
    }
    
      //function definition
    function getAge (address _personIdentifier) onlyBy() payable external returns (uint) {
       
       human =  myStruct("Ritesh",10,true,new uint[](3)); //using struct myStruct
       
       gender _gender = gender.male; //using enum 
       
       ageRead(personIdentifier, stateIntVariable);
    }
~~~

### 事件
~~~solidity
    // event declaration
    event ageRead(address, int );
~~~

### 枚举
~~~solodity
    //enumeration declaration
    enum gender {male, female}
    
    gender _gender=gender.male
~~~
### 方法
限定符

public:这种可见性使得函数可以直接从外部访问。它们成为合约接口的一部分，可以在内部和外部调用。

internal:默认情况下，如果没有指定，则状态变量具有 internal限定符。这意味着此函数只能用于当前合约以及任何从其继承的合约。这些函数不能从外部访问，它们不是合约接口的一部分。

private:私有函数只能在声明它们的合约中使用，即使在派生合约中0也不能使用它们。它们不是合约接口的一部分。

external:这种可见性使得函数可以直接从外部但不是内部访问。这些函数是合约接口的一部分。

附加限定符

constant 这些函数不具有修改区块链状态的能力 可以读取状
态变量并返回给调用者，但不能修改任何变量、触发事件、创建另一个
合约、调用其他可以改变状态的函数等 将常函数看作可以读取和返回
当前状态变量值的函数

view 这些函数是常量函数的别名

pure : pure 函数进一步限制了函数的能力 pure 函数既不能读取也
不能写人，即它们不能访问状态变量 使用此限定符声明的函数应确保
它们不会访问当前状态和交易变量

payable ：使用 payab le 关键字声 明的函数能够接受来自调用者的以
太币 如果发送者没有提供以太币，则调用将会失败 如果一个函数被
标记为 payable ，该函数只能接受以太币

### 数据类型
这两种类型在变量赋值和存储在 EVM 中的方式方面有所不同。可以通过创建一个新副本或者仅仅通过处理引用来完成变量的赋值。值类型维护变量的独立副本，并且在一个变量中更改值不会影响另一个变量中的值。但是，更改引用类型变量中的值可确保任何引用该变量的地方都会获取更新值。
值类型
![image.png](https://note.youdao.com/yws/res/5131/WEBRESOURCEc5eb2a6b1281d715dd49ba4607650248)
引用类型
![image.png](https://note.youdao.com/yws/res/5135/WEBRESOURCEd869e65f1f2c51f6133a20c0c21cd4a9)
