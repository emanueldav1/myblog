def f(nums):
    n = len(nums)
    s = set()
    dup = None
    for x in nums:
        if x in s:
            dup = x
        s.add(x)
    total = n * (n + 1) // 2
    missing = total - (sum(nums) - dup)
    return (dup, missing)
