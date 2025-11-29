def f(x, y):
    n=len(x)
    mx=sum(x)/n
    my=sum(y)/n
    num=sum((x[i]-mx)*(y[i]-my) for i in range(n))
    den=sum((x[i]-mx)**2 for i in range(n))
    a=num/den
    b=my-a*mx
    return [b, a]
