def f(x):
    res=[]
    nums="123456789"
    def dfs(i, expr):
        if i==9:
            if eval(expr)==x:
                res.append(expr+"=="+str(x))
            return
        dfs(i+1, expr+"+"+nums[i])
        dfs(i+1, expr+"-"+nums[i])
        dfs(i+1, expr+nums[i])
    dfs(1, nums[0])
    return res
