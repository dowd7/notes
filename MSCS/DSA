```python
def twoWayMerge(lst1, lst2):
    # Merge two sorted lists into a single sorted list.
    
    n1 = len(lst1)
    n2 = len(lst2)
    
    if n1 == 0:
        return list(lst2)
    elif n2 == 0:
        return list(lst1)
    else:
        output_lst = []
        i=0
        j=0
        while (i < n1 or j < n2):
            if i < n1 and j < n2:
                if (lst1[i] <= lst2[j]):
                    output_lst.append(lst1[i])
                    i = i + 1   
                else:
                    output_lst.append(lst2[j])
                    j = j + 1
            elif i < n1:
                output_lst.append(lst1[i])
                i = i + 1
            else: 
                output_lst.append(lst2[j])
                j = j + 1
        return output_lst
    
list1 = [1, 3, 5, 7, 9]
list2 = [2, 4, 6, 8, 10]

print(twoWayMerge(list1, list2)) 
```
