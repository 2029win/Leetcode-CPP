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





2...........移除元素
给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素。元素的顺序可能发生改变。然后返回 nums 中与 val 不同的元素的数量。

假设 nums 中不等于 val 的元素数量为 k，要通过此题，您需要执行以下操作：

更改 nums 数组，使 nums 的前 k 个元素包含不等于 val 的元素。nums 的其余元素和 nums 的大小并不重要。       //这一块很重要，只注意数组前k项，其他的不用管，使得代码中109行的出现
返回 k。
用户评测：

评测机将使用以下代码测试您的解决方案：

int[] nums = [...]; // 输入数组
int val = ...; // 要移除的值
int[] expectedNums = [...]; // 长度正确的预期答案。
                            // 它以不等于 val 的值排序。

int k = removeElement(nums, val); // 调用你的实现

assert k == expectedNums.length;
sort(nums, 0, k); // 排序 nums 的前 k 个元素
for (int i = 0; i < actualLength; i++) {
    assert nums[i] == expectedNums[i];
}
如果所有的断言都通过，你的解决方案将会 通过。

 

示例 1：

输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2,_,_]
解释：你的函数应该返回 k = 2, 并且 nums 中的前两个元素均为 2。
你在返回的 k 个元素之外留下了什么并不重要（因此它们并不计入评测）。
示例 2：

输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,4,0,3,_,_,_]
解释：你的函数应该返回 k = 5，并且 nums 中的前五个元素为 0,0,1,3,4。
注意这五个元素可以任意顺序返回。
你在返回的 k 个元素之外留下了什么并不重要（因此它们并不计入评测）。



我的答案
int removeElement(int* nums, int numsSize, int val) {
    int i;
    int j=0;
    for(i=0;i<numsSize;i++)
    {
if(nums[i]!=val)
{
    nums[j]=nums[i];
j++;
}
    }
    return j;
}

3.............有序数组的平方
给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

 

示例 1：

输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]
示例 2：

输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]

/**
 * Note: The returned array must be malloced, assume caller calls free().///////////“题目要求：你返回的数组必须是用 malloc 申请的；我们（调用你这个函数的人）会负责调用 free() 来释放你返回的数组。”
 */
int* sortedSquares(int* nums, int numsSize, int* returnSize) {
    int i;
    int* res = (int*)malloc(sizeof(int) * numsSize);//堆区申请一块新内存给调用者。这样调用者 free(res) 的时候，就是在合法释放堆内存，大家都安全，不在原数组上做修改，不用自己写free函数，这是调用者用的。
    *returnSize =numsSize;////必须这样写，因为第135行是出题人自己给的，不能不用
    for(i=0;i<numsSize;i++)
    {
        res[i]=nums[i]*nums[i];
    }
    for(i=0;i<numsSize;i++)
    {
       for(int j=0;j<numsSize-1-i;j++)
       {
        if(res[j]>res[j+1])
        {
            int temp=res[j];
            res[j]=res[j+1];
            res[j+1]=temp;
        }
       }
    }
    return res;
}

 4.............长度最小的子数组
 给定一个含有 n 个正整数的数组和一个正整数 target 。

找出该数组中满足其总和大于等于 target 的长度最小的 子数组 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。//////////意思是从1到之后n项或从j到之后的x项，其中n和x可以是符合标准的任意值。

 

示例 1：

输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。
示例 2：

输入：target = 4, nums = [1,4,4]
输出：1
示例 3：

输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
 

提示：

1 <= target <= 109
1 <= nums.length <= 105
1 <= nums[i] <= 104
 
 
 答案（官方答案）
 int minSubArrayLen(int s, int* nums, int numsSize) {
    if (numsSize == 0) {
        return 0;
    }
    int ans = INT_MAX;//////////代表int类型能存的最大值（通常是 2147483647），是一个超大的数。如果循环结束后ans还是这个超大数，就说明全程没找到符合条件的子数组。
    for (int i = 0; i < numsSize; i++) {
        int sum = 0;
        for (int j = i; j < numsSize; j++) {
            sum += nums[j];
            if (sum >= s) {
                ans = fmin(ans, j - i + 1);////// j- i + 1：子数组的长度计算公式。j 是结束下标，i 是起始下标，比如 i=4、j=5，长度就是 5-4+1=2，和示例 1 的结果一致。
fmin(a,b)：C 语言<math.h>里的函数，作用是取两个数里更小的那个。这里就是把「当前找到的子数组长度」和「之前记录的最小长度 ans」对比，取更小的那个更新 ans。
                break;
            }
        }
    }
    return ans == INT_MAX ? 0 : ans;////////如果ans最终还是等于初始的INT_MAX：说明循环全程没找到任何符合条件的子数组，返回 0；
否则：返回我们找到的、所有符合条件的子数组里的最小长度ans。
}




















