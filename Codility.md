# Codility

## Binary gap


```python
def sol(N):
    N = bin(N)[2:]
    b = 0
    maxb = 0
    for k in N:
        if int(k) == 0:
            b += 1
        elif int(k) == 1:
            maxb = max(b,maxb)
            b = 0
    return maxb

sol(int(input('Num int a bin y encontrar el binary gap max ')))
```

    Num int a bin y encontrar el binary gap max 12123425235





    2




```python
def sol(N):
    return len(max(format(N, 'b').strip('0').split('1')))
sol(int(input('Num int a bin y encontrar el binary gap max ')))
```

    Num int a bin y encontrar el binary gap max 9





    2



## Cyclic rotation


```python
def sol(A,K):
    N = len(A)
    B = [None]*N
    for i in range(0,N):
        B[(i+K)%N] = A[i]
    return B
    pass

K = 3
A = [3,8,9,7,6]
sol(A,K)
```




    [9, 7, 6, 3, 8]



## Odd occurrences in array


```python
def sol(A):
    A = sorted(A)
    print(A)
    for i in range(0,len(A),2):
        if A[i] != A[i+1]:
            return A[i]
            
A = [9,3,5,6,5,3,9]
sol(A)
```

    [3, 3, 5, 5, 6, 9, 9]





    6



## Frog jump


```python
x = 1
y = 7
D = 2
def sol(x,y,D):
    v = (y-x)//D
    if x+v*D >= y:
        return v
    else:
        return v+1
    pass

sol(x,y,D) #Doesn't have to be precise jumps
```




    3



## Perm missing element


```python
A = [2,3,1,5] #Smallest element is 1 and largest one is N+1

def sol(A):
    A.sort()
    for i in range(0,len(A)):
        if A[i] != i+1:
            return i+1
    return (len(A)+1)

def sol2(A):
    A.sort()
    for i in range(len(A)):
        if i+1 != A[i]:
            return i+1
    return (len(A)+1)

sol(A)
#sol2(A)
```




    4



## Tape equilibrium


```python
A = [3,1,2,4,3]
    # We want to find the min value of the abs diff
    # of the sum of the left/right side of the array
def sol(A):
    s = sum(A)
    mindiff = 2000
    sl = 0
    for i in range(0,len(A)-1):
        sl += A[i]
        diff = abs(sl-s+sl)
        mindiff = min(mindiff,diff)
    return mindiff

sol(A)
```




    1



## Frog river one


```python
def sol(X,A):
    B = [-1]*X
    for i in range(len(A)):
        if A[i] <= X and B[A[i]-1] == -1:
            B[A[i]-1] = i
    m = 0
    for i in range(len(B)):
        if B[i] == -1:
            return -1
        m = max(m,B[i])
    return m
pass

A = [1,1,2,5,3,4,3]
X = 5

sol(X,A)
            
```




    5



## Max counter


```python
A = [3,4,4,6,1,4,4]
N = 5

def sol(N,A):
    S = [0]*N
    m = 0
    for i in range(len(A)):
        if A[i] > N:
            S = [m for x in S]
        else:
            S[A[i]%N-1] += 1 
        m = max(S)
    return S
    
sol(N,A)
```




    [3, 2, 2, 4, 2]




```python
A = [3,4,4,6,1,4,4]
print(A[len(A)-1])
```

    4


## Missing positive integer


```python
A=[1,3,6,4,1,2]
def sol(A):
    A.sort()
    if A[len(A)-1]<0:
        return 1
    for i in range(len(A)-1):
        if A[i]>0 and A[i+1]-A[i]>1:
            return A[i]+1
    return A[len(A)-1]+1

sol(A)
```




    5



## Perm check


```python
A = [4,1,3,2,-1]
def sol(A):
    A = [x for x in A if x>=0]
    A.sort()
    for i in range(len(A)):
        if A[i] != i+1:
            return 0
    return 1
    
sol(A)
```




    1



## Count divisibles


```python
A,B,K = 100,123000000,2
def sol(A,B,K):
    S = list(range(A,B+1))
    c=0
    for i in range(len(S)):
        if S[i]%K == 0:
            c += 1
    return c
sol(A,B,K)
```




    61499951




```python
A,B,K = 100,1230000057455634560,22312331534533
def sol(A,B,K):
    c = int(B/K)-int(A/K)
    if A%K == 0:
        c += 1
    return c
sol(A,B,K)
```




    55126



## Genomic range


```python
S = 'CAGCCTA'
P = [2,5,0]
Q = [4,5,6]
def sol(S, P, Q):
    ans = []
    for (p, q) in zip(P,Q):
        if 'A' in S[p:q+1]:
            ans.append(1)
        elif 'C' in S[p:q+1]:
            ans.append(2)
        elif 'G' in S[p:q+1]:
            ans.append(3)
        else:
            ans.append(4)         
    return ans
sol(S, P, Q)
```




    [2, 4, 1]



## MinAvgTwoSlice


```python
def sol(A): #100%
    mini = max(A)*2
    mi = 0 #random big/small values
    for i in range(len(A)-2):
        v1 = (A[i]+A[i+1]+A[i+2])/3
        v2 = (A[i]+A[i+1])/2
        if mini>v1 or mini>v2:
            mini = min(v1,v2)
            mi = i
    if mini>(A[-1]+A[-2])/2:    #edge case
        return len(A)-2
    return int(mi)
    pass
A = [4,2,2,5,1,5,8]
sol(A)
```




    1




```python
A = [4,2,2,5,1,5,8]
def sol(A):
    mini = max(A)*2
    mi = 0 #random big/small values
    for i in range(len(A)-1):
        for j in range(1,len(A)):
            if i != j and i+1<j:
                v = sum(A[i:j])/len(A[i:j])
                if v < mini:
                    mini = v
                    mi = i
    return int(mi)
sol(A)          
```




    1



## Passing cars


```python

```
