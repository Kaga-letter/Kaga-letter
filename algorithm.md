#### 动态规划——字符串问题

**最长公共连续子序列：**

```c++
int longestCommonSubsequence(string text1, string text2) {
     int len1=text1.length(),len2=text2.length();
     vector<vector<int>>dp(len1+1,vector<int>(len2+1,0));
     for(int  i=1;i<len1+1;i++)
        for(int j=1;j<len2+1;j++)
        {
            if(text1[i-1]==text2[j-1])
            dp[i][j]=dp[i-1][j-1]+1;
            else
            dp[i][j]=max(dp[i][j-1],dp[i-1][j]);
           
        }
        return dp[len1][len2];
    }
```

**最长回文子序列：**

```c++
int longestPalindromeSubseq(string s) {
        int len=s.length();
        vector<vector<int>>dp(len,vector<int>(len,0));
        for(int i=0;i<len;i++)
         {
             dp[i][i]=1;
             for(int j=i-1;j>=0;j--)
             {
                 if(s[i]==s[j])
                 dp[j][i]=dp[j+1][i-1]+2;
                 else
                 dp[j][i]=max(dp[j+1][i],dp[j][i-1]);
             }

         }
         return dp[0][len-1];

    }
```

**最长回文子串：**

```c++
string longestPalindrome(string s) {
        if(s.length()<2)
        return s;
    vector<vector<int>>dp(s.length(),vector<int>(s.length(),0));
    int maxlen=1,start=0;
    for(int i=0;i<s.length();i++)
    dp[i][i]=1;
    for(int j=1;j<s.length();j++)
        for(int i=0;i<j;i++)
        {
            
            if(s[i]!=s[j])
            dp[i][j]=0;
            else
            {
                if(j-i<3)
                dp[i][j]=1;
                else
                dp[i][j]=dp[i+1][j-1];
               
            }
             if(j-i+1>maxlen&&dp[i][j])
                {
                    maxlen=j-i+1;
                    start=i;
                }
        }
        
        return s.substr(start,maxlen);
       
    }
```



#### 字符串匹配

##### 朴素算法

```c++
int strStr(string haystack, string needle) {
        if(needle.size()==0)
        return 0;
        if(haystack.size()==0||needle.size()>haystack.size())
        return -1;
       for(int i=0;i<=haystack.length()-needle.length();i++)
       {
           int j=i,k=0;
           while(k<needle.length()&&haystack[j]==needle[k])
           {
               j++;
               k++;
           }
           if(k==needle.length())
           return i;


       }
       return -1;
    }
```

##### KMP算法

```c++
int strStr(string haystack, string needle) {
        int n=haystack.size();
        int m=needle.size();
        if(m==0)
            return 0;
        vector<int> next(m);
        //预处理next数组
        for(int j=0,i=1;i<m;i++){
            while(j&&needle[i]!=needle[j]) j=next[j-1];  
            if(needle[i]==needle[j]) j++;
            next[i]=j;
        }
        //匹配过程
        for(int i=0,j=0;i<n;i++){
            while(j&&haystack[i]!=needle[j]) j=next[j-1];
            if(haystack[i]==needle[j]) j++;
            //因为字符串下标从0开始，因而结果需要加一
            if(j==m) return i-m+1;
        }
        return -1;
    }
```

#### 排序算法

**快排：**

```c++
int once_quick_sort(vector<int>&v,int left,int right)
{
    int key=v[left];
    while(left<right)
    {
        while(left<right&&key<=v[right])
        {
            right--;
        }
        if(left<right)
        {
            v[left++]=v[right];
        }
        while(left<right&&key>=v[left])
        {
            left++;
        }
        if(left<right)
        {
            v[right--]=v[left];
        }
       
    }
     v[left]=key;
    return left;
}
int quick_sort(vector<int>&v,int left,int right)
{
    if(left>=right)
        return 1;
    int mid = once_quick_sort(v, left, right);
    quick_sort(v,left,mid-1);
    quick_sort(v,mid+1,right);
 }
```


