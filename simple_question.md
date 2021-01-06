1. 给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

示例 1:

输入: 123
输出: 321
 示例 2:

输入: -123
输出: -321
示例 3:

输入: 120
输出: 21
注意:

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。

A：

    int reverse(int x){
    int i = 1,cent,y,sum = 0,p,j = 0;
    int A[10]={2,1,4,7,4,8,3,6,4,7};
    int B[10]={-2,-1,-4,-7,-4,-8,-3,-6,-4,-8};
      cent = x;
  //位数计算   
    
    while(cent!=0&&(cent>=10||cent<=-10)){
            cent=cent/10;
            i=i*10;
                             }
  //合法性判断
          
    cent = x;
         if(i==1000000000){
              int tag=1;
              while(cent!=0){
              y=cent%10;
              cent=cent/10;
      
        if(y>A[j]||y<B[j])
          if(tag)
           return 0;
        if((y<A[j]&&y>0)||(y>B[j]&&y<0))
           tag=0;
        j++;
         }
         
     }    
    cent = x;
 //逆转部分
 
    while(cent!=0){
        y=cent%10;
        cent=cent/10;
        p=y*i;
        sum=sum+p;
        i=i/10;
        }
    return sum;
     }
