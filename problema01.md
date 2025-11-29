
  definição f(números, alvo):

    vistos = {}  
    
    for i, num in enumerate(nums):
        complemento = alvo - num
        
        
        if complemento in vistos:
            
            return (vistos[complemento], i)
        
        
        vistos[num] = i
