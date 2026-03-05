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




5....................区间和
题目描述
给定一个整数数组 Array，请计算该数组在每个指定区间内元素的总和。
输入描述
第一行输入为整数数组 Array 的长度 n，接下来 n 行，每行一个整数，表示数组的元素。随后的输入为需要计算总和的区间下标：a，b （b > = a），直至文件结束。
输出描述
输出每个指定区间内元素的总和。
输入示例
5
1
2
3
4
5
0 1
1 3
输出示例
3
9
提示信息
数据范围：
0 < n <= 100000


官方答案：
#include <stdio.h>
int main()
{
    int n;
    scanf("%d",&n);
    int arr[n];//////////////放在scanf的后面
    int preSum[n+1];/////创建新变量，为了在后面把下标0-n的和求出来
    preSum[0] = 0;

    for(int i=0;i<n;i++)
    {
        scanf("%d",&arr[i]);
        preSum[i+1]=arr[i]+preSum[i];
    }
     int a,b;
     while(scanf("%d %d",&a,&b)!=EOF)///符合题目的直至文件结束。
     {
         int sum=preSum[b+1]-preSum[a];///为求a-b区间内的和
         printf("%d\n",sum);
     }
return 0;
}


.6.........
在一个城市区域内，被划分成了n * m个连续的区块，每个区块都拥有不同的权值，代表着其土地价值。目前，有两家开发公司，A 公司和 B 公司，希望购买这个城市区域的土地。 

现在，需要将这个城市区域的所有区块分配给 A 公司和 B 公司。

然而，由于城市规划的限制，只允许将区域按横向或纵向划分成两个子区域，而且每个子区域都必须包含一个或多个区块。 为了确保公平竞争，你需要找到一种分配方式，使得 A 公司和 B 公司各自的子区域内的土地总价值之差最小。 

注意：区块不可再分。

输入描述
第一行输入两个正整数，代表 n 和 m。 

接下来的 n 行，每行输出 m 个正整数。

输出描述
请输出一个整数，代表两个子区域内土地总价值之间的最小差距。
输入示例
3 3
1 2 3
2 1 3
1 2 3
输出示例
0


#include <stdio.h>
#include <limits.h>
int main()
{
    int n,m;
    scanf("%d %d",&n,&m);
    int arr[n][m];
    int i,j;
    int total_sum=0;
    for(i=0;i<n;i++)
    {
        for(j=0;j<m;j++)
        {
            scanf("%d",&arr[i][j]);
            total_sum += arr[i][j];////////////为下面简单
        }
    }
    int sum1=0,sum2=0;
    int ans = INT_MAX;
    for(i=1;i<n;i++)
    {
        int a;
         for(j=0;j<m;j++)
         {
            sum1=sum1+arr[i-1][j];
                 
         }
         if(sum1*2-total_sum>=0)
         {
            a=sum1*2-total_sum;
         }
         else{a=total_sum-sum1*2;}
       ans = fmin(ans, a);
    }///////////sum1不重复赋值为0，可以使sum1表示为前n行的总和
 for(j=1;j<m;j++)
    {
          int a;
         for(i=0;i<n;i++)
         {
            sum2=sum2+arr[i][j-1];
         }
         if(total_sum-sum2*2>=0)
         {
            a=total_sum-sum2*2;
         }
         else{a=sum2*2-total_sum;}
         ans = fmin(ans, a);
    }
     printf("%d\n", ans);
return 0;


}




7...螺旋矩阵

给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

 

示例 1：


输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
示例 2：

输入：n = 1
输出：[[1]]
 
官方答案
int** generateMatrix(int n, int* returnSize, int** returnColumnSizes) {
    int maxNum = n * n;    //最大数
    int curNum = 1;    //当前要填入矩阵的数字，从 1 开始，每填充一个数就自增 1，直到等于maxNum。
    int** matrix = malloc(sizeof(int*) * n);  //给二级指针matrix分配内存，申请n个int*类型的空间，也就是给矩阵的n个行指针分配空间，每个行指针后续会指向矩阵的一行数据。
    *returnSize = n;
    *returnColumnSizes = malloc(sizeof(int) * n);
    for (int i = 0; i < n; i++) {
        matrix[i] = malloc(sizeof(int) * n);
        memset(matrix[i], 0, sizeof(int) * n);  //：核心关键！把第i行的所有元素初始化为 0。 我们填充的数字是从 1 开始的，因此0就代表这个位置未被填充，后续转向判断会依赖这个标记。
        (*returnColumnSizes)[i] = n;  //给输出参数赋值，告诉调用者矩阵的第i行有n列。   方括号 [] 的优先级比星号 * 高。
//////如果不加括号，写成 *returnColumnSizes[i]，编译器会理解成：
/////先算 returnColumnSizes[i]（把 returnColumnSizes 当成数组取下标）。
/////再对结果取 *。
/////这是错的！ 会导致程序崩溃。
    }
    int row = 0, column = 0;
    int directions[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};  // 右下左上 //注意是{0，1}不是（0，1）.意思是第一行有两个数 分别是0 1 
    int directionIndex = 0; //当前方向的索引，初始值为 0，对应第一个方向「向右」，符合螺旋从左到右填充第一行的逻辑。
    while (curNum <= maxNum) {
        matrix[row][column] = curNum;
        curNum++;
        int nextRow = row + directions[directionIndex][0], nextColumn = column + directions[directionIndex][1]; //// 预判下一个位置，判断是否需要转向
        if (nextRow < 0 || nextRow >= n || nextColumn < 0 || nextColumn >= n || matrix[nextRow][nextColumn] != 0) {   //// 越界/已填充 → 顺时针转向
            directionIndex = (directionIndex + 1) % 4;  // 顺时针旋转至下一个方向
        }
        row = row + directions[directionIndex][0];   //// 更新到下一个要填充的位置
        column = column + directions[directionIndex][1];
    }//循环的核心逻辑：先填充当前位置，再预判下一个位置，不能走就转向，最后走到下一个位置，直到所有数字填充完毕。
    return matrix;
}


