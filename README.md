# Day2
写了一道力扣，明天得努力了

https://leetcode.cn/problems/minimum-size-subarray-sum/description/
给定一个含有 n 个正整数的数组和一个正整数 target 。

找出该数组中满足其总和大于等于 target 的长度最小的 连续子数组 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

我用的是二分查找＋前缀数组的办法
用sums[i]把输入数组nums的前n项和加在一起，然后从i开始查找结果满足的值，每次把最小值存在ans里面，最后输出ans。
学会了auto bound = lower_bound(nums.begin(),nums.end(),target)来返回大于等于目标值的迭代器的代码。
看了解决答案：
class Solution {
public:
    int minSubArrayLen(int s, vector<int>& nums) {
    int  n = nums.size();
    if(n==0){
        return 0;
    }
    int ans = INT_MAX;
    vector<int> sums(n+1,0);
    for(int i =1;i<=n;i++){
        sums[i]=sums[i-1]+nums[i-1];
    }
    for(int i =1;i<=n;i++){
        int target = s+sums[i-1];
        auto bound = lower_bound(sums.begin(),sums.end(),target);
        if(bound!= sums.end()){
            ans = min(ans,static_cast<int>(bound-sums.begin())-(i-1));
        }
    }
    return ans == INT_MAX?0:ans;
    }
};
