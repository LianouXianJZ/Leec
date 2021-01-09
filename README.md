# Leec
That‘s really boring...

1.   使用revert *= 10 ；revert += temp%10 可以避免定义过多变量，以及显示计算需要倒转的整数的位数。 

2.   对于二维字符串数组，首先通过*p=s[i]取得第一维，再通过*(p+j)取得第二维。需要返回二维数组地址时，可通过 char *p = s[0]; return p;
