## TARO
> TARO开发中遇到的问题和小技巧

1 . 初始化变量这里最好初始化声明为 `null`，初始化又不赋值的话
小程序可能会报警为变量为 undefined
```bash
   let token = null;
```
2 . 