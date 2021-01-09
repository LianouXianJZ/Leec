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

2.判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:

输入: 121
输出: true
示例 2:

输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
示例 3:

输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。

A:

    /*该方法有溢出风险*/
    bool isPalindrome(int x){
         //int型会溢出
         long int invert,temp;
         temp = x;
         invert = 0 ;
         //将数字倒转
         while(temp){
          invert *= 10;
          invert += temp%10;
          temp=temp/10;
         }
        if((invert-x==0&&x>0)||(x==0))
          return true;
        else 
        return false;

     }
     
3.最长公共前缀
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

示例 1:

输入: ["flower","flow","flight"]
输出: "fl"
示例 2:

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
说明:

所有输入只包含小写字母 a-z 。

A：

    char * longestCommonPrefix(char ** strs, int strsSize){
    if(strsSize==0)
    return "";
    if(strsSize==1){
        char *q=strs[0];
        return q;
    }
    int i=0,j=0,tag;
    char A[150];
    A[0]=NULL;
    char *p=&A;
    while(1){
    for(i=0;i<strsSize-1;i++){
        tag=strs[i][j]-strs[i+1][j];
        if(tag!=0||strs[i][j]=='\0'){
            return p;
        } 
    }
    A[j]=strs[0][j];
    A[j+1]='\0';
    j++;
    }

    }
