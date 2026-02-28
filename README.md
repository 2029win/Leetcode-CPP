# Leetcode-CPP
刷题11111111111111111111
给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

示例 1:

输入: nums = [-1,0,3,5,9,12], target = 9     
输出: 4       
解释: 9 出现在 nums 中并且下标为 4     
示例 2:

输入: nums = [-1,0,3,5,9,12], target = 2     
输出: -1        
解释: 2 不存在 nums 中因此返回 -1        
提示：

你可以假设 nums 中的所有元素是不重复的。
n 将在 [1, 10000]之间。
nums 的每个元素都将在 [-9999, 9999]之间。

我答案
#include <stdio.h>
int search(int* nums, int size, int target) {
    int j = size - 1;
    int m;
    while (i <= j)
    {
        m = i  + (j - i) / 2;//相当于（i+j）/2，只不过为了防止超过最大阈值写的。  二分查找，必须记
        if (target < nums[m])//注意是nums【m】，而不是单个m。
        {
            j = m - 1;
        }
        else if (target == nums[m])
        {
            return m;
        }
        else {
            i = m + 1;
        }

    }
    return -1;//返回值为-1可以表明若输入值不为数组中的任意一个，也就是没找到的意思。
}
int main()
{
    int arr[] = { -1,0,3,5,9,12 };
    int n;
    scanf_s("%d", &n);
    int a = search(arr, 6, n);
    printf("%d", a);
    return 0;
}


























