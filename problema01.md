
[problem_01 (1).py](https://github.com/user-attachments/files/23834714/problem_01.1.py)
def f(nums, alvo):
    
    vistos = {}  
    
    for i, num in enumerate(nums):
        complemento = alvo - num
        
        
        if complemento in vistos:
            
            return (vistos[complemento], i)
        
        
        vistos[num] = i

