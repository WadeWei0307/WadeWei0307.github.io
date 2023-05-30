---
#此區稱為front-matter
title: leetcode Experience
description: 紀錄程式自我學習 #butterfly.yml中 index_post_content 調整, 文章封面會顯示此段文字
date: 2022-11-01 19:18:00
categories: 
  - Code Training
  - LeetCode
cover: /image/leetcode-Experience/leetcode_coverImg.png #/blog/source
tags:
keywords:
abbrlink:
top_img:
#此區稱為front-matter
---

# Easy Part
## Array 相關問題
### Q1 - Top Interview
* <font color="red"> 題目：</font>給定一個vector nums和一個int target，必須在vector內的元素找到兩個相加等於target的位置。<br>
[原題目連結](https://leetcode.com/problems/two-sum/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```
2. <br>
```text
Input: nums = [3,2,4], target = 6
Output: [1,2]
```
* <font color="red">想法：</font>將與target的差值存進Hash table內，若vector內的元素有在Hash table則代表找到兩個元素的位置。<br>
```c++=
vector<int> leetcode_1::twoSum(vector<int>& nums, int target) {
    map<int, int> diffIndx; //{nums[i], i}
    for (int i = 0; i < nums.size(); i++) {
        if (!diffIndx.count(target - nums[i])) //judge whether (target - nums[i]) is in diffIndx or not
            diffIndx[nums[i]] = i;
        else
            return { diffIndx[target - nums[i]], i };
    }
    return { 0, 0 }; //if find no any combination
}
```
* <font color="red">時間複雜度：</font>走訪一次nums，所以O(n)。<br>
### Q26 - Top Interview
* <font color="red"> 題目：</font>給一個non-decreasing order的 vector nums，要移除相同的元素，並回傳剩餘元素的個數。<br>
[原題目連結](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```
2. <br>
```text
Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```
* <font color="red">想法：</font>因為是non-decreasing order，所以只要下一個value大於原先的value，則表示沒重複，並且把下一個的位置記下來(finalSize)。<br>
```c++=
int leetcode_26::removeDuplicates(vector<int>& nums) {
    int finalSize = 1; //return finally size
    for (int i = 1; i < nums.size(); i++) { 
        if (nums[i] > nums[i - 1]) { //because is sorted array, so can use >
            nums[finalSize] = nums[i]; //record the finalSize and value of finalSize
            ++finalSize;
        }
    }
    return finalSize;
}
```
* <font color="red">時間複雜度：</font>走訪一次nums，所以O(n)。<br>
### Q27
* <font color="red"> 題目：</font>給定一個陣列，必須在同一個陣列內移除相同的元素，並且回傳陣列內剩餘的個數。<br>
[原題目連結](https://leetcode.com/problems/remove-element/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [3,2,2,3], val = 3 
Output: 2, nums = [2,2,_,_] 
```
2. <br>
```text
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
```
* <font color="red">想法：</font>若遇到陣列內元素與val相等則刪除，且陣列長度同時-1。<br>
```c++=
int leetcode_27::removeElement_27(vector<int>& nums, int val) {
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] == val) {
            nums.erase(nums.begin() + i);
            --i; //刪掉一個長度會-1，所以也要讓index-1
        }
    }
    return nums.size();
}
```
* <font color="red">時間複雜度：</font>走訪一次nums，所以O(n)。<br>
### Q35
* <font color="red"> 題目：</font>給一個vector nums和一個int target，必須找到target要在排序好的nums的哪個位置。<br>
特殊要求：必須在O(log(n))完成。<br>
[原題目連結](https://leetcode.com/problems/search-insert-position/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [1,3,5,6], target = 5
Output: 2
```
2. <br>
```text
Input: nums = [1,3,5,6], target = 2
Output: 1
```
3. <br>
```text
Input: nums = [1,3,5,6], target = 7
Output: 4
```
* <font color="red">想法：</font>因為必須在O(log(n))完成，所以必須用binary search達成。<br>
```c++=
int leetcode_35::searchInsert(vector<int>& nums, int target) {
    int start = 0;
    int end = nums.size() - 1;
    int mid;
    while (start <= end) { //O(log(n)) need to use binary search
        mid = (start + end) / 2;
        if (target == nums[mid]) {
            return mid;
        }
        else if (target > nums[mid]) {
            start = mid + 1;
        }
        else
            end = mid - 1;
    }
    return start;
}
```
* <font color="red">時間複雜度：</font>binary search，所以O(log(n))。<br>
### Q66 - Top Interview
* <font color="red"> 題目：</font>給一個vector digits，必須把裡頭的元素當成int加1。<br>
[原題目連結](https://leetcode.com/problems/plus-one/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].
```
2. <br>
```text
Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].
```
3. <br>
```text
Input: digits = [9]
Output: [1,0]
Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].
```
* <font color="red">想法：</font>利用carryBit判斷是否有進位，分成兩種情形：<br>
1. 如果某位數不是9，則carryBit清成False(避免在迴圈外又再最大位數insert一個1)，並且跳出迴圈。<br>
2. 如果全部都是9，則在跳出迴圈時，必須在最大位數insert一個1。<br>
```c++=
vector<int> leetcode_66::plusOne(vector<int>& digits) {
    bool carryBit = false;
    for (int i = digits.size() - 1; i >= 0; i--) {
        if (i == digits.size() - 1 && digits[i] == 9) { //個位數是9
            carryBit = true;
            digits[i] = 0;
        }
        else if (digits[i] == 9 && carryBit) { //十位數以上有9且有進位
            digits[i] = 0;
        }
        else {
            carryBit = false; //避免該位數不是9的時候又在後面digits.insert 
            digits[i] += 1;
            break;
        }
    }
    if (carryBit) //表示前面全部都是9
        digits.insert(digits.begin(), 1);
    return digits;
}
```
* <font color="red">時間複雜度：</font>走訪一次digits，所以O(n)。<br>
### Q88 - Top Interview
* <font color="red"> 題目：</font>給vector nums1及該vector實際上有value的個數m，以及vector nums2及該vector實際上有value的個數n(也等於nums2.size())，必須將兩個vector合併且是non-decreasing order vector。<br>
特殊要求：不得宣告其餘空間，只能回傳nums1。<br>
[原題目連結](https://leetcode.com/problems/merge-sorted-array/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
```
2. <br>
```text
Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].
```
3. <br>
```text
Input: nums1 = [0], m = 0, nums2 = [1], n = 1
Output: [1]
Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.
```
* <font color="red">想法：</font><br>
1. 將nums2最大的元素與nums1最大的元素開始比，若nums2大，則將nums2放在最後一個；反之則將nums1的放在最後一個，以此類推。
2. 當然也可以直接將nums2先放在nums1後面，然後再sort。
```c++=
void leetcode_88::merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    int i = nums1.size() - 1;
    if (m == 0) { //nums1 is empty
        nums1 = nums2;
    }
    else {
        while (m > 0 && n > 0) { //nums1 or nums2都還有Element還沒比完的時候
            if (nums2[n - 1] > nums1[m - 1]) { //當nums2的元素比nums1的元素大，把nums2的元素往後擺在nums1的後面
                nums1[i] = nums2[n - 1];
                --i;
                --n;
            }
            else { //當nums1的元素比nums2的大，把nums1的元素往後擺
                nums1[i] = nums1[m - 1];
                --i;
                --m;
            }
        }
    }
    for (int j = 0; j < n; j++) { //若nums2全部元素都比nums1最小的還小的時候
        nums1[j] = nums2[j];
    }
}
```
* <font color="red">時間複雜度：</font><br>
1. 若為想法1，則為走訪一個nums1 or nums2，所以為O(n)。<br>
2. 若為想法2，則最快的排序只能到達O(log(n))。<br>
### Q108 - Top Interview
* <font color="red"> 題目：</font>將給定的vector nums1轉成binary tree。<br>
[原題目連結](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:
```
2. <br>
```text
Input: nums = [1,3]
Output: [3,1]
Explanation: [1,null,3] and [3,1] are both height-balanced BSTs.
```
* <font color="red">想法：</font> 利用binary search以及遞迴的方式將左子樹和右子樹建立起來。
```c++=
class TreeNode {
public:
    int val;
    TreeNode* left;
    TreeNode* right;
public:
    TreeNode(): val(0), left(NULL), right(NULL) {}
    TreeNode(int x): val(x), left(NULL), right(NULL) {}
    TreeNode(int x, TreeNode* left, TreeNode* right) : val(x), left(left), right(right) {}
};
TreeNode* leetcode_108::sortedArrayToBST(vector<int>& nums) {
    return binarySearch(nums, 0, nums.size() - 1);
}
TreeNode* leetcode_108::binarySearch(vector<int>& nums, int start, int end) {
    if (start > end)
        return NULL;
    TreeNode* root = new TreeNode();
    int mid = (start + end) / 2 ;
    root->val = nums[mid];
    root->left = binarySearch(nums, start, mid-1);
    root->right = binarySearch(nums, mid + 1, end);
    return root;
}
```
* <font color="red">時間複雜度：</font>每個binarySearch function為O(log(n))，nums裡的每個元素都會走一次binarySearch function，所以為O(nlog(n))。
### Q118 - Top Interview
* <font color="red"> 題目：</font>給一個整數n，回傳巴斯卡三角形前n層所有組合。<br>
[原題目連結](https://leetcode.com/problems/pascals-triangle/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```
2. <br>
```text
Input: numRows = 1
Output: [[1]]
```
* <font color="red">想法：</font>a[n][n] = a[n-1][n-1] + a[n-1][n]。
```c++=
vector<vector<int>> leetcode_118::generate(int numRows) {
    int hypotenuse = 1; //斜邊
    vector<vector<int>> ans;
    vector<int> tempAns;
    for (int level = 1; level <= numRows; level++) {
        int lastestIndex = level - 1; //該層最後一個Index
        int preLevel = level - 2; //前一層的值
        for (int indexOfLevel = 0; indexOfLevel < level; indexOfLevel++) {
            if (indexOfLevel == 0 || indexOfLevel == lastestIndex) //如果是第一個Index或當前Level的最後一個Index
                tempAns.push_back(hypotenuse);
            else {
                int exIndex = indexOfLevel - 1; //記錄前一個Index
                tempAns.push_back(ans[preLevel][exIndex] + ans[preLevel][indexOfLevel]);
            }
        }
        ans.push_back(tempAns);
        tempAns.clear();
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>每個level遍歷所有元素一次，故O(n<sup>2</sup>)。
### Q119
* <font color="red"> 題目：</font>給一個整數n，回傳巴斯卡三角形第n層的組合。<br>
[原題目連結](https://leetcode.com/problems/pascals-triangle-ii/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: rowIndex = 3
Output: [1,3,3,1]
```
2. <br>
```text
Input: rowIndex = 0
Output: [1]
```
3.<br>
```text
Input: rowIndex = 1
Output: [1,1]
```
* <font color="red">想法：</font>如註解所示。
```c++=
vector<int> leetcode_119::getRow(int rowIndex) {
//           n!
// nCr = -----------
//        r!.(n-r)!

//                  n!
// nC(r-1) = -----------------
//            (r-1)!.(n-r+1)!

//                     n!        (r-1)!x(n-r+1)!
// nCr / nC(r-1) = ----------- x ---------------
//                  r!.(n-r)!          n!

//                 (n-r+1)
//               = -------
//                    r

// nC0 = 1
// nCr = nC(r-1) x (n-r+1) / r
    vector<int> ans(rowIndex + 1, 1);
    int temp = 1;
    for (int i = 1; i < rowIndex; i++) {
        temp = temp * (rowIndex - i + 1) / i;
        ans[i] = temp;
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>只需把第n層的每個係數算出來，所以O(n)。
### Q121 - Top Interview
* <font color="red"> 題目：</font>給一個vector，n個元素表示n日的股價，算出最大的收益<br>
[原題目連結](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```
2. <br>
```text
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```
* <font color="red">想法：</font>每遍歷一次元素便判斷是否為最低點，若不是則計算一次收益，若是最低點則替換掉原先的最低點且不必計算收益。
```c++=
int leetcode_121::maxProfit(vector<int>& prices) {
    int profit = 0; //最後收益
    int tmpProfit = 0; //算暫時的收益
    int lowest = prices[0]; // 最低點
    for (int i = 1; i < prices.size(); i++) {
        if (prices[i] >= lowest) { //如果比最低點大，算一次收益
            tmpProfit = prices[i] - lowest;
            if (tmpProfit > profit) { //如果此次收益比原本的收益大，取代掉
                profit = tmpProfit;
            }
        }
        else //此次為更低點
            lowest = prices[i];
    }
    return profit;
}
```
* <font color="red">時間複雜度：</font>遍歷每天的股價，所以O(n)。
### Q136 - Top Interview
* <font color="red"> 題目：</font>給一段vector，判斷只出現過一次的元素，其餘皆剛好出現兩次<br>
[原題目連結](https://leetcode.com/problems/single-number/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [2,2,1]
Output: 1
```
2. <br>
```text
Input: nums = [4,1,2,1,2]
Output: 4
```
3. <br>
```text
Input: nums = [1]
Output: 1
```
* <font color="red">想法：</font>因為其餘元素剛好只出現過兩次，所以可以利用XOR(互斥或)。
```c++=
int leetcode_136::singleNumber(vector<int>& nums) {
    int ans = nums[0];
    for (int i = 1; i < nums.size(); i++) {
        ans = ans ^ nums[i]; //因為重複的元素只會出現兩次，所以可以用互斥或
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>遍歷每個元素，所以O(n)。
### Q169 - Top Interview
* <font color="red"> 題目：</font>給一段vector，找出出現最多次的元素<br>
[原題目連結](https://leetcode.com/problems/majority-element/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [3,2,3]
Output: 3
```
2. <br>
```text
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```
* <font color="red">想法：</font>出現過最多次的元素一定會>=長度的一半。
```c++=
int leetcode_169::majorityElement(vector<int>& nums) {
        int count = 1; //數數字出現幾次
        int majority = nums[0];
        for (int i = 1; i < nums.size(); i++) { //因為majority一定>=nums.size()/2，所以減到最後一定剩下majority
            if (majority == nums[i])
                count++;
            else
                count--;
            if (count == 0) { //count被扣成0換人當majority
                majority = nums[i];
                count = 1;
            }
        }
        return majority;
}
```
* <font color="red">時間複雜度：</font>遍歷每個元素，所以O(n)。
### Q217 - Top Interview
* <font color="red"> 題目：</font>給一段vector，如果有出現重複則回傳TRUE，反之則FALSE。<br>
[原題目連結](https://leetcode.com/problems/contains-duplicate/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [1,2,3,1]
Output: true
```
2. <br>
```text
Input: nums = [1,2,3,4]
Output: false
```
* <font color="red">想法：</font>利用hash table的library -> count()。
```c++=
bool leetcode_217::containsDuplicate(vector<int>& nums) {
    map<int, bool> existElement; //紀錄是否出現過
    for (int i = 0; i < nums.size(); i++) {
        if (!existElement.count(nums[i]))
            existElement[nums[i]] = true;
        else
            return true;
    }
    return false;
}
```
* <font color="red">時間複雜度：</font>遍歷每個元素，且Hash table搜尋為O(1)，所以O(n)。
### Q219
* <font color="red"> 題目：</font>給一段vector，如果有出現重複且兩個元素所在的位置其距離小於等於整數K，若存在多個重負責取距離最短的，則回傳TRUE；反之則FALSE。<br>
[原題目連結](https://leetcode.com/problems/contains-duplicate-ii/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [1,2,3,1], k = 3
Output: true
```
2. <br>
```text
Input: nums = [1,0,1,1], k = 1
Output: true
```
3. <br>
```text
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```
* <font color="red">想法：</font>利用hash table記住元素以及其位置。
```c++=
bool leetcode_219::containsNearbyDuplicate(vector<int>& nums, int k) {
    map<int, int> elementIndex; //記得元素的位置
    int lengthOfElement = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (!elementIndex.count(nums[i]))
            elementIndex[nums[i]] = i;
        else { //若存在此元素，則計算兩個重複的元素距離
            lengthOfElement = i - elementIndex[nums[i]];
            elementIndex[nums[i]] = i;
            if (k >= lengthOfElement)
                return true;
        }
    }
    return false;
}
```
* <font color="red">時間複雜度：</font>遍歷每個元素，且Hash table搜尋為O(1)，所以O(n)。
### Q228
* <font color="red"> 題目：</font>給一段vector，每個數字只會出現一次，若連續的數字則整理成"a->b"，若單獨出現則整理成"a"。<br>
[原題目連結](https://leetcode.com/problems/summary-ranges/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
Explanation: The ranges are:
[0,2] --> "0->2"
[4,5] --> "4->5"
[7,7] --> "7"
```
2. <br>
```text
Input: nums = [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
Explanation: The ranges are:
[0,0] --> "0"
[2,4] --> "2->4"
[6,6] --> "6"
[8,9] --> "8->9"
```
* <font color="red">想法：</font>跟題目所述一樣。
```c++=
vector<string> leetcode_228::summaryRanges(vector<int>& nums) {
    vector<string> ans;
    int startIndex = 0; //記住每一次的起點
    if (nums.size() < 1) //若nums沒有任何的元素
        return ans;
    for (int i = 0; i < nums.size(); i++) {
        if (i == nums.size() - 1 || nums[i] + 1 != nums[i + 1]) { //處理是最後一個元素的時候無條件進入；在不是最後一個元素時判斷前一個跟下一個不是連續的元素
            if (i - startIndex > 0) { //起點跟終點有至少1個數量以上的元素
                ans.push_back(to_string(nums[startIndex]) + "->" + to_string(nums[i]));
                startIndex = i + 1; //將起點移至終點的下一個元素
            }
            else { //起點跟終點是同一個元素
                ans.push_back(to_string(nums[startIndex]));
                startIndex = i + 1; //將起點移至終點的下一個元素
            }
        }
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>遍歷每個元素，所以O(n)。
### Q268 - Top Interview
* <font color="red"> 題目：</font>給一vector的整數，找出少掉的數字。<br>
[原題目連結](https://leetcode.com/problems/missing-number/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.
```
2. <br>
```text
Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.
```
3. <br>
```text
Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.
```
* <font color="red">想法：</font>先將Range內的所有數字加總，再減去input vector內的數字加總。
```c++=
int leetcode_268::missingNumber(vector<int>& nums) {
    int totalCount = nums.size();
    int ans;
    ans = ((0 + totalCount) * (totalCount-0+1)) / 2; //先總和nums長度
    for (int i = 0; i < nums.size(); i++) { 
        ans -= nums[i]; //再減去nums裡面的所有元素
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>遍歷每個元素，所以O(n)。
### Q283 - Top Interview
* <font color="red"> 題目：</font>給一vector排序好的整數，最後將0移到vector後方。<br>
[原題目連結](https://leetcode.com/problems/move-zeroes/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```
2. <br>
```text
Input: nums = [0]
Output: [0]
```
* <font color="red">想法：</font>遇到非0的元素則跟第0的index元素交換，並且將index移到1。
```c++=
void leetcode_283::moveZeroes(vector<int>& nums) {
    int lastNonZero = 0; 
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] == 0)
            continue;
        else { //遇到不為0的從前面第一個開始放，並且記錄最後一個不為0的位置
            nums[lastNonZero++] = nums[i]; //這裡也可以用交換的，如此一來就不用再用後面的迴圈把0補上去 swap(nums[lastNonzero], nums[i]); lastNonzero++;
        }
    }
    for (int i = lastNonZero; i < nums.size(); i++) { //從不為0的位置開始後面都放0
        nums[i] = 0;
    }
}
```
* <font color="red">時間複雜度：</font>遍歷每個元素，所以O(n)。
### Q303
* <font color="red"> 題目：</font>給一vector整數，且input left跟right，回傳sum(left,right)這個範圍內的總合。<br>
[原題目連結](https://leetcode.com/problems/range-sum-query-immutable/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input
["NumArray", "sumRange", "sumRange", "sumRange"]
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]
Output
[null, 1, -1, -3]

Explanation
NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
numArray.sumRange(0, 2); // return (-2) + 0 + 3 = 1
numArray.sumRange(2, 5); // return 3 + (-5) + 2 + (-1) = -1
numArray.sumRange(0, 5); // return (-2) + 0 + 3 + (-5) + 2 + (-1) = -3
```
* <font color="red">想法：</font>先將資料處理好，a[0]為前0個元素的總和，a[1]為前1個元素的總和，以此類推。
```c++=
class leetcode_303 {
public:
    vector<int> tmpAns;
public:
    leetcode_303(vector<int>& nums) {
        tmpAns.resize(nums.size(), nums[0]);
        for (int i = 1; i < nums.size(); i++) { //tmpAns存放累加值
            tmpAns[i] = nums[i]+tmpAns[i-1]; //當下的值+前面的累加值
        }
    }
    int sumRange(int left, int right);
};
int leetcode_303::sumRange(int left, int right) {
    return left == 0 ? tmpAns[right]:tmpAns[right] - tmpAns[left-1];
}
```
* <font color="red">時間複雜度：</font>因為資料已經事先處理好，所以在回傳總和時可以達到O(1)。
### Q349
* <font color="red"> 題目：</font>給兩個vector整數，找出兩個vector出現過一樣的整數。<br>
[原題目連結](https://leetcode.com/problems/intersection-of-two-arrays/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```
2. <br>
```text
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.
```
* <font color="red">想法：</font>利用Hash table紀錄每個元素是否出現過，再去與第二個vector做比對。
```c++=
vector<int> leetcode_349::intersect(vector<int>& nums1, vector<int>& nums2) {
    map<int, bool> elementExist;
    vector<int> ans;
    for (int i = 0; i < nums1.size(); i++) { //將nums1出現過的元素存進hash table並設成TRUE
        if (!elementExist.count(nums1[i]))
            elementExist[nums1[i]] = true;
    }
    for (int i = 0; i < nums2.size(); i++) { //將nums2曾經出現在nums1的元素推進ans，並且只推一次
        if (elementExist[nums2[i]]) {
            ans.push_back(nums2[i]);
            elementExist[nums2[i]] = false;
        }
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>遍歷兩個vector各一次，所以O(n)。
### Q350
* <font color="red"> 題目：</font>給兩個vector整數，找出兩個vector出現一樣多次的整數。<br>
[原題目連結](https://leetcode.com/problems/intersection-of-two-arrays-ii/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```
2. <br>
```text
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.
```
* <font color="red">想法：</font>利用Hash table紀錄每個元素出現的次數，再去與第二個vector做比對。
```c++=
vector<int> leetcode_350::intersect_2(vector<int>& nums1, vector<int>& nums2) {
    map<int, int> m; //用來記錄nums1元素個出現幾次
    vector<int> ans;
    for (int i = 0; i < nums1.size(); i++) { //將nums1的出現個數記錄在m
        if (!m.count(nums1[i]))
            m[nums1[i]] = 1;
        else
            m[nums1[i]]++;
    }
    for (int i = 0; i < nums2.size(); i++) { //用nums2的個數去比對m裡面的出現次數
        if (m.count(nums2[i]) && m[nums2[i]] > 0) { //若nums2在m裡出現且次數>0
            ans.push_back(nums2[i]);
            m[nums2[i]]--;
        }
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>遍歷兩個vector各一次，所以O(n)。
### Q448
* <font color="red"> 題目：</font>給一個1-n長的vector，找出1-n沒出現過的數字<br>
[原題目連結](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)<br>
* <font color="red">範例：</font><br>
1. <br>
```text
Input: nums = [4,3,2,7,8,2,3,1]
Output: [5,6]
```
2. <br>
```text
Input: nums = [1,1]
Output: [2]
```
* <font color="red">想法：</font>
1. 可利用set，將出現過的數字存入set，再利用set跑1-n的迴圈判斷1-n誰沒出現過。<font color="orange">(時間較慢)</font>
2. 利用兩個vector <font color="orange">速度較快</font>。
```c++=
vector<int> leetcode_448::findDisappearedNumbers(vector<int>& nums) {
    vector<bool> vote(nums.size() + 1, false); //因為需要1~nums.size的空間，所以需要+1
    vector<int> ans;
    for (int i = 0; i < nums.size(); i++) { //將出現過的數字n於vote的第n個位置變成TRUE
        if (!vote[nums[i]])
            vote[nums[i]] = true;
    }
    for (int i = 1; i <= nums.size(); i++) { //從1~nums.size找出vote為false的位置
        if (!vote[i])
            ans.push_back(i);
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>遍歷nums vector一次以及vote vector一次，所以O(n)。
### Q463
* <font color="red"> 題目：</font>找出圍起來的陸地的周長。<br>
[原題目連結](https://leetcode.com/problems/island-perimeter/)<br>
* <font color="red">範例：</font><br>
{% asset_img leet_463.PNG leetcode 463 image %}
1.  <br>
```text
Input: grid = [[0,1,0,0],[1,1,1,0],[0,1,0,0],[1,1,0,0]]
Output: 16
Explanation: The perimeter is the 16 yellow stripes in the image above.
```
2. <br>
```text
Input: grid = [[1]]
Output: 4
```
3. <br>
```text
Input: grid = [[1,0]]
Output: 4
```
* <font color="red">想法：</font>row major遍歷二維vector，若出現前後陸地，則總周長要-2；反之column major的時候也一樣，因為前一個陸地被重複算了一次，且下一個連著的陸地也被重複算一次周長。
```c++=
int leetcode_463::islandPerimeter(vector<vector<int>>& grid) {
    int ans = 0;
    int totalDuplicateSide = 0;
    int xDuplicateSide;
    int yDuplicateSide;
    for (int i = 0; i < grid.size(); i++) { //row major遍歷二維vector
        xDuplicateSide = 0;
        for (int j = 0; j < grid[0].size(); j++) {
            if (j > 0) { //因為有可能第0行有陸地，且必須列入計算周長+4
                int preY = j - 1;
                if (grid[i][j] == 1 && grid[i][preY] == 1) {//如果此塊為陸地，且其前一行也為陸地
                    ans += 4;
                    xDuplicateSide += 1;
                }
                else if (grid[i][j] == 1)
                    ans += 4;
            }
            else if (grid[i][j] == 1)
                ans += 4;
        }
        if (xDuplicateSide > 0) //減去row major連續出現陸地的次數*2
            ans -= xDuplicateSide * 2;
    }
    for (int i = 0; i < grid[0].size(); i++) { //column major遍歷二維vector
        yDuplicateSide = 0;
        for (int j = 1; j < grid.size(); j++) {
            int preX = j-1;
            if (grid[j][i] == 1 && grid[preX][i] == 1) {//如果此塊為陸地，且其前一列也為陸地
                yDuplicateSide += 1;
            }
        }
        if (yDuplicateSide > 0) //減去column major連續出現陸地的次數*2
            ans -= yDuplicateSide * 2;
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>遍歷兩次二維vector，所以O(n<sup>2</sup>)。
# Medium Part
## Array 相關問題
### Q11 - Top Interview
* <font color="red"> 題目：</font>給一個vector整數表示數根柱子，找出可以裝出最多水的體積。<br>
[原題目連結](https://leetcode.com/problems/container-with-most-water/)<br>
* <font color="red">範例：</font><br>
{% asset_img leet_11.PNG leetcode 11 image %}
1.  <br>
```text
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```
2. <br>
```text
Input: height = [1,1]
Output: 1
```
* <font color="red">想法：</font>從前面及後面同時進行，每次找短的柱子算一次面積，並且由短的柱子那邊向前或向後找下一根柱子。
```c++=
int leetcode_11::maxArea(vector<int>& height) {
    int start = 0;
    int end = height.size() - 1;
    int width = height.size() - 1;
    int ans = 0;
    int tmpArea;
    if (height.size() < 2) //沒有兩根柱子以上
        return 0;
    while (end > start) { //直到兩根重疊
        if (height[start] > height[end]) { //取短的那根當長
            tmpArea = height[end] * width;
            end--; //短的那邊往前找更長的
        }
        else { //取短的那根當長
            tmpArea = height[start] * width;
            start++; //短的那邊往後找更長的
        }
        width--;
        if (tmpArea > ans)
            ans = tmpArea;
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>幾乎都是要遍歷全部柱子，所以O(n)。
### Q49 - Top Interview
* <font color="red"> 題目：</font>給一個vector字串，將裡面的字元全部一樣的字串分成一組。<br>
[原題目連結](https://leetcode.com/problems/group-anagrams/)<br>
* <font color="red">範例：</font><br>
1.  <br>
```text
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```
2. <br>
```text
Input: strs = [""]
Output: [[""]]
```
3. <br>
```text
Input: strs = ["a"]
Output: [["a"]]
```
* <font color="red">想法：</font>先將字串排序，確保不管遇到什麼順序的字母都會唯一存在，將出現過的存進hash table，並設為group 1，因為唯一存在，所以下個出現不一樣的字串一定與其他不一樣，所以設為group 2，以此類推。
```c++=
vector<vector<string>> leetcode_49::groupAnagrams(vector<string>& strs) {
    vector<vector<string>> ans;
    map<string, int> m;
    string s;
    int group = 0;
    for (int i = 0; i < strs.size(); i++) {
        s = strs[i];
        sort(s.begin(),s.end()); //對字串排序，ex: eat -> aet
        if (!m.count(s)) { 
            m[s] = group++; //因為排序後，所以找到的字串不管怎麼交換順序一定不一樣
            ans.push_back({ strs[i] });
        }
        else 
            ans[m[s]].push_back(strs[i]); //找到排序後重複的，直接取value值，看它屬於哪個group
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>sort為O(nlogn)，再加上遍歷strs一遍O(n)，所以O(n<sup>2</sup>logn)。
### Q122 - Top Interview
* <font color="red"> 題目：</font>給一個vector整數當作每天的股價，在這幾天內得到最大的收益。<br>
[原題目連結](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)<br>
* <font color="red">範例：</font><br>
1.  <br>
```text
Input: prices = [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
```
2. <br>
```text
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Total profit is 4.
```
3. <br>
```text
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.
```
* <font color="red">想法：</font>透過累加的方式將小收益變成總收益。
```c++=
int leetcode_122::maxProfit2(vector<int>& prices) {
    int profit = 0;
    for (int i = 1; i < prices.size(); i++) {
        if (prices[i] > prices[i - 1]) //只需要計算下一天比前一天大的收益並且累加起來，也會是最大的收益
            profit += prices[i] - prices[i - 1];
    }
    return profit;
}
```
* <font color="red">時間複雜度：</font>遍歷一次vector完成，所以O(n)。
### Q137
* <font color="red"> 題目：</font>給一個vector整數，且每個整數都剛好出現3次，除了一個獨立的數字只出現一次，要找出此獨立的數字。<br>
[原題目連結](https://leetcode.com/problems/single-number-ii/)<br>
* <font color="red">範例：</font><br>
1.  <br>
```text
Input: nums = [2,2,3,2]
Output: 3
```
2. <br>
```text
Input: nums = [0,1,0,1,0,1,99]
Output: 99
```
* <font color="red">想法：</font>統計每個bit為1的個數，若不為3的倍數，則表示獨立的數字該bit也為1；不用考慮bit為0的情況，因為就算count為0，也會被3整除。
```c++=
int leetcode_137::singleNumber2(vector<int>& nums) {
    unsigned int shift = 1; //用來判定每個bit是1是0
    int count; //用來記錄有幾個數字該bit為1
    unsigned int ans = 0; 
    for (int i = 0; i < 32; i++) { //32個bits
        count = 0;
        for (auto num : nums) {
            if (num & shift) //判斷該bit是否為1
                count++;
        }
        if (count % 3 != 0) {//如果count為0，表示每個num該bit都是0，也會被整除；如果沒被3整除，則表示獨立的數字該bit為1
            ans |= shift; //將bit用or組起來
        }
        shift <<= 1; //左移換檢查下一個bit
    }
    return ans;
}
```
* <font color="red">時間複雜度：</font>第一個for為常數時間O(32) = O(1)，第二個為遍歷vector nums，所以O(1) * O(n) = O(n)。
## Dynamic Programming 相關問題
### Q62 - Top Interview
* <font color="red"> 題目：</font>給兩個int，分別代表長(n)和寬(m)，從左上角走到右下角，途中只能往右或往下的方法有幾種<br>
[原題目連結](https://leetcode.com/problems/unique-paths/)<br>
* <font color="red">範例：</font><br>
1.  <br>
{% asset_img leet_62.jpg leetcode 463 image %}
```text
Input: m = 3, n = 7
Output: 28
```
2. <br>
```text
Input: m = 3, n = 2
Output: 3
Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
```
* <font color="red">想法：</font>
1.將每個方向(R or D)想像成必須組合他們已到達目的地，如：RRRDD(m=3,n=4)，他就是5!/3!2!，從前者公式可以看出其為：(n*(n+1)*...*(n+m-2)) / (1*...*(m-1))。
2.其實這是一題DP的題目，他可以從計算每格的步數來算出最後到達目的地的步數，但這裡是用較快的數學方式寫法。
```c++=
int leetcode_62::uniquePaths(int m, int n) {
    int molecular = m - 1; //(分子)
    int denominator = n - 1; //(分母)
    double sum = 1.0; //avoid have double like = 3/2 in operation
    for (int i = 1; i <= molecular; i++) {
        sum = sum * (denominator + i) / i;
    }
    return (int)sum;
}
```
* <font color="red">時間複雜度：</font>走一個寬度或長度，故O(n-1) or O(m-1)。