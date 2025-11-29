def f(x, y):
    r = []
    for a, b in zip(x, y):
        r += [a, b]
    return r
