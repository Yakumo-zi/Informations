# Programming Language

## PL-A

### Week_2

类型检查先于执行

表达式必须是递归的，可以有任意深度

每个表达式都有三种规则：

1. 语法规则：如何书写这个表达式
2. 类型规则：子表达式允许使用什么类型，表达式的返回类型是什么，static enviroment
3. 执行求值规则：如何执行表达式,dynamic enviroment

```
less than:

if e1 < e2 then e3 then e4;

type-checking:
	first e1 and e2 should be of the same type,or they can undergo a comparison.next e3 and e4 should be same type.
	
evaluation:
	first the value of e1 is v1,value of e2 is v2.Comparing v1 and v2 will yield a boolean result.if it is ture,value of e3 is v3 will be returned,otherwise value of e4 is v4 will be returned.
```

#### Five different things

* Syntax: how do you write language constructs?
* **Semantics**: what do programs mean? (Type-checking rules,Evaluation rules)
* **Idioms**: what are typical patterns for using language features to express your computation?
* Libraries: what facilities does the language provide "standard"?
* Tools: what do language implementations provide to make your job easier?