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
4.括号匹配问题
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

A：

    bool isValid(char * s){
    //可用strlen计算s长度
    char A[4000];
    A[0]='1';
    int i=0,j=0;
    if(s[0]==NULL)
    {
        return true;
    }
    else{
        A[0]=s[0]; 
        while(s[i+1]!='\0'){
        //处理第一组匹配导致的栈空问题
            if(j==-1){
                A[j+1]=s[i+1];
                j++;
                i++;
            }
        //无需进行正则匹配，相邻的括号的asc值为确定值
        else if(s[i+1]-A[j]==1||s[i+1]-A[j]==2){
                A[j]=0;
                j--;
                i++;
            }
            else{  
                A[j+1]=s[i+1];
                j++;
                i++;
            }
        }
    if(j==-1)
    return true;
    else
    return false;
    }
    }

5.升序链表链接

     struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
    struct ListNode *p = (struct ListNode *)malloc(sizeof(struct ListNode));
    struct ListNode *q=p;
    if(l1==NULL&&l2==NULL){
        return 0;
    }
    while(1){
        //都不为空
        if(l1!=NULL&&l2!=NULL){
            if(l1->val>l2->val){
            struct ListNode *r = (struct ListNode *)malloc(sizeof(struct ListNode));
            r->val=l2->val;
            r->next=NULL;
            q->next=r;
            q=q->next;
            l2=l2->next;
            }
            else if(l1->val<l2->val){
            struct ListNode *r = (struct ListNode *)malloc(sizeof(struct ListNode));
            r->val=l1->val;
            r->next=NULL;
            q->next=r;
            q=q->next;
            l1=l1->next;   
            }
            else if(l1->val==l2->val){
                for(int i=0;i<2;i++){
            struct ListNode *r = (struct ListNode *)malloc(sizeof(struct ListNode));
            r->val=l1->val;
            r->next=NULL;
            q->next=r;
            q=q->next;
                }
                l1=l1->next;
                l2=l2->next;
            }
        }
        //其中一个先为空
        else if(l1==NULL&&l2==NULL){
            return p->next;
        }
        //另一个为空
       else if(l1==NULL&&l2!=NULL){
           q->next=l2;
           return p->next;
       }
       else if(l2==NULL&&l1!=NULL){
           q->next=l1;
           return p->next;
       }
    }
    }


6.数组去重
给定一个排序数组，你需要在 原地 删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

 

示例 1:

给定数组 nums = [1,1,2], 

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 

你不需要考虑数组中超出新长度后面的元素。
示例 2:

给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。

A：  


    int removeDuplicates(int* nums, int numsSize){
    if(numsSize==0)
        return numsSize;
    else if(numsSize==1)
        return 1;
    else{
        int k=0,tag=1,per=0;
        for(int i=0;i<numsSize-1;i++){
            if(nums[i+1]!=nums[i]){
                if(tag==1){
                    per++;
                }
                else{
                    nums[per+1]=nums[i+1];
                    per++;
                }
            }
            else{
                k++;
                tag=0;
            }
        }
        return numsSize-k;
    }
    }
7.两数相加

给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。


A：

  
  
        struct ListNode* cre_N(struct ListNode *p){
    p=(struct ListNode *)malloc(sizeof(struct ListNode));
    p->next=NULL;
    return p;
    }
    struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    struct ListNode *p,*r,*q;
    p=cre_N(p);
    r=p;
    int a,b,tag=0;
    while(l1!=NULL||l2!=NULL){
        if(l1!=NULL){
            a=l1->val;
            l1=l1->next;
        }
        else{
            a=0;
        }
        if(l2!=NULL){
            b=l2->val;
            l2=l2->next;
        }
        else{
            b=0;
        }
        q=cre_N(q);
        q->val=(a+b+tag)%10;
        r->next=q;
        r=r->next;
        if((a+b+tag)%10!=(a+b+tag)){
        tag=1;
        }
        else{
            tag=0;
        }   
    }
    if(tag==1){
           q=cre_N(q);
           q->val=1;
           r->next=q;
        }
    return p->next;
    }


8.最大子序和

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:

输入: [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。


A：

     //指针所指之前元素之和小于零就丢弃
    int maxSubArray(int* nums, int numsSize){
    int Max=nums[0],per=0,B_Max;
    B_Max=Max;
    for(int i=1;i<numsSize;i++){
        if(Max<=0){
            per++;
            Max=nums[i];
        }
        else{
            Max = Max+nums[i];
        }
        if(Max>B_Max)
        B_Max=Max;
    }
    return B_Max;
    }
    
9.示例 1：

输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2
示例 2：

输入：nums1 = [1,2], nums2 = [3,4]
输出：2.50000
解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
示例 3：

输入：nums1 = [0,0], nums2 = [0,0]
输出：0.00000
示例 4：

输入：nums1 = [], nums2 = [1]
输出：1.00000
示例 5：

输入：nums1 = [2], nums2 = []
输出：2.00000




A:  给定两个大小为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的中位数。
   
   
   
    //屎一样的代码
    double findMedianSortedArrays(int* nums1, int nums1Size, int* nums2, int nums2Size){
    //两序列和为奇数
    int pre1=0,pre2=0,tag=0,temp;
    int A[(nums1Size+nums2Size)/2+1];
    int f=(nums1Size+nums2Size)/2+1;
    //return 0;
    while(tag<=(nums1Size+nums2Size)/2){
        if(pre1<=nums1Size-1&&pre2<=nums2Size-1){
            if(nums1[pre1]>nums2[pre2]){
                A[tag] = nums2[pre2];
                pre2++;
                tag++;
            }
            else if(nums1[pre1]<nums2[pre2]){
                A[tag] = nums1[pre1];
                pre1++;
                tag++;
            }
            else if(nums1[pre1]==nums2[pre2]){
                A[tag] = nums1[pre1];
                if(tag+1<f)
                A[tag+1]=nums1[pre1];
                pre1++;
                pre2++;
                tag+=2;
                
            }
        }
        else if(pre1>nums1Size-1){
            A[tag] = nums2[pre2];
            pre2++;
            tag++;    
        }
        else if(pre2>nums2Size-1){
            A[tag] = nums1[pre1];
            pre1++;
            tag++;
        }
    }
    int c=(nums1Size+nums2Size)/2;
    if((nums1Size+nums2Size)%2!=0)
       return A[c];
    else
    return (A[c-1]+A[c])/2.0;
    }

