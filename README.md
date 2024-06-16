class Solution:
    def findMedianSortedArrays(self, nums1, nums2):
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1
        n, m = len(nums1), len(nums2)
        imin, imax, half_len = 0, n, (n + m + 1) // 2
        while imin <= imax:
            i = (imin + imax) // 2
            j = half_len - i
            if i < n and nums1[i] < nums2[j - 1]:
                imin = i + 1
            elif i > 0 and nums1[i - 1] > nums2[j]:
                imax = i - 1
            else:
                if i == 0:
                    max_of_left = nums2[j - 1]
                elif j == 0:
                    max_of_left = nums1[i - 1]
                else:
                    max_of_left = max(nums1[i - 1], nums2[j - 1])
                if (n + m) % 2 == 1:
                    return max_of_left
                if i == n:
                    min_of_right = nums2[j]
                elif j == m:
                    min_of_right = nums1[i]
                else:
                    min_of_right = min(nums1[i], nums2[j])
                return (max_of_left + min_of_right) / 2.0
