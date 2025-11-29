def f(prices):
    m=prices[0]
    lucro=0
    for p in prices:
        if p<m:
            m=p
        lucro=max(lucro,p-m)
    return lucro
