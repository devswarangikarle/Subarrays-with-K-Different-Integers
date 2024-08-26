# Subarrays-with-K-Different-Integers

Given an integer array nums and an integer k, return the number of good subarrays of nums.
A good array is an array where the number of different integers in that array is exactly k.
For example, [1,2,3,1,2] has 3 different integers: 1, 2, and 3.
A subarray is a contiguous part of an array.

Constraints:
1 <= nums.length <= 2 * 104
1 <= nums[i], k <= nums.length

class Solution:
    def subarraysWithKDistinct(self, nums, k):
        return self.subarraysWithAtMostKDistinct(nums, k) - self.subarraysWithAtMostKDistinct(nums, k - 1)

    def subarraysWithAtMostKDistinct(self, nums, k):
        ans = 0
        count = [0] * (len(nums) + 1)

        l = 0
        for r in range(len(nums)):
            count[nums[r]] += 1
            if count[nums[r]] == 1:
                k -= 1
            while k == -1:
                count[nums[l]] -= 1
                if count[nums[l]] == 0:
                    k += 1
                l += 1
            ans += r - l + 1
        return ans
