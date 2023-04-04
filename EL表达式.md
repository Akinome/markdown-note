# EL表达式

## 什么是EL表达式

EL表达式全称是：Expression Language。主要作用是替代 jsp 页面中的表达式脚本在 jsp 页面中进行数据的输出。

## EL表达式如何使用

语法：${表达式}

### 运算符

1. 关系运算
2. 逻辑运算
3. 算数运算
4. empty运算
5. 三元运算
6. "."点运算 和 [] 中括号运算符 (是去找key值对应的get的方法)

### 隐式对象

1. pageContext

2. Scope:范围/作用域

3. pageScope

4. requestScope

5. sessionScope

6. applicationScope

7. paramValues

8. hearder

9. cookie

10. initParam

注意：最大application 最小page 一般情况可省略

param 必要参数不可以省略 对象获取参数

## 页尾
