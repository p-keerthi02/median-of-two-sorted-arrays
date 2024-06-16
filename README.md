class Solution:
    def findMedianSortedArrays(self, nums1, nums2):
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1
        n, m = len(nums1), len(nums2)
        i, j, half_len = 0, n, (n + m + 1) // 2
        while i <= j:
            x = (i + j) // 2
            y = half_len - i
            if x < n and nums1[x] < nums2[y - 1]:
                i = x + 1
            elif x > 0 and nums1[x - 1] > nums2[y]:
                j = x - 1
            else:
                if x == 0:
                    max_of_left = nums2[y - 1]
                elif y == 0:
                    max_of_left = nums1[x - 1]
                else:
                    max_of_left = max(nums1[x - 1], nums2[y - 1])
                if (n + m) % 2 == 1:
                    return max_of_left
                if x == n:
                    min_of_right = nums2[y]
                elif y == m:
                    min_of_right = nums1[x]
                else:
                    min_of_right = min(nums1[x], nums2[y])
                return (max_of_left + min_of_right) / 2.0
