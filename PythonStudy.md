# Python Hacking Study Note

## Study Resource

* [Introduction to Python](https://drive.google.com/file/d/1zVO65QK8t0CUzD7vjcMbLwOTtRi1AFYO/view)
* [The Python Tutorial](https://docs.python.org/3/tutorial/index.html)

## 1. Ready to Learn
* Python character
  - interpreter language
    
## 2. Basic
A. Values = data
1) Mission 1
```python
userName = input("what is your name? ")
print("Good morning, " + userName + "!")
print("I like fruits. How about you?")
userFruit = input("Do you have a favorite? ")
print("OK. You like " + userFruit + "!")
print("I prepare " + userFruit + " for you!")
```

B. Data type
C. Boolean
D. List
```python
dataList = [1, "seungho", "apple"]
rint(dataList[2])
addData = input("Add data? ")
dataList.append(addData)
print(dataList)
dataList.remove("apple")
print(dataList)
```
* The len() function returns the number of items in an object.

2) Mission 2
```python
userInfo = []
userName = input("what is your name? ")
userInfo.append(userName)
print("Good morning, " + userInfo[0] + "!")
print("I like fruits. How about you?")
userFruit = input("Do you have a favorite? ")
userInfo.append(userFruit)
print("OK. You like " + userInfo[1] + "!")
print("I prepare " + userInfo[1] + " for " + userInfo[0] + " !")
```

E. tuple
- it cannot change data
F. Dictionary
- Saving Key, values
```python
data = {"name":"seungho", "fruit":"apple"}
data["email"] = "test@test.com"
del(data["fruit"])
```

3) Mission 3
```python
userInfo = {}
userInfo["userName"] = input("what is your name? ")
print("Good morning, " + userInfo["userName"] + "!")
print("I like fruits. How about you?")
userInfo["userFruit"] = input("Do you have a favorite? ")
print("OK. You like " + userInfo["userFruit"] + "!")
print("I prepare " + userInfo["userFruit"] + " for you!")
```

##  3. Control Code
A. if statement
1) mission 4
```python
score = int(input("What is your score?"))
if (score == 100):
    print ("Very Good")
elif (score < 100 and score >= 80):
    print ("Good")
elif (score < 80 and score >= 40):
    print ("Need to work on")
elif (score >= 0 and score < 40):
    print ("What are you doing?")
else:
    print ("Input correct score!!")
```
B. Exception
- try: (execute code) except: (error code) exit()
C. repeat
- while

2) mission 5
```python
while (True):
    cmd = input("> ")
    if (cmd == "exit"):
        break
    if (len(cmd) >  10):
        print("wrong commend")
        continue
    
    print("Working" + cmd)
```
D. for
```python
numList = [1,2,3,4,5,6,7,8,9,10]
numList1 = range(1,11)
for num in numList:
  print(num)
```

3) mission 6
```python
for num in range(1,101):
    if (num % 2 == 0):
        print(str(num) + ": even")
    else:
        print("{}: odd".format(num))
```

## 4. Useful Code
1) Function
- a block of program statements which can be used repetitively in a program
2) Mission 7
- up down game
```python
com_num = 77
life = 5
def updownGame(com_num, user_num):
    if(user_num > com_num):
        print("Down")
    elif (user_num < com_num):
        print("Up")
    else:
        return True
while (life > 0):
    print("You have {} chance".format(life))
    user_num = int(input("input number:"))
    gameRes = updownGame(com_num, user_num)
    if(gameRes):
        print("Success")
        exit()
    life -= 1
print("You lose")
```
3) library = import

## 5. Final mission
```python
import random as r
com_num = r.randrange(1,101)
life = 5
def updownGame(com_num, user_num):
    if(user_num > com_num):
        print("Down")
    elif (user_num < com_num):
        print("Up")
    else:
        return True
while (life > 0):
    print("You have {} chance".format(life))
    user_num = int(input("input number:"))
    gameRes = updownGame(com_num, user_num)
    if(gameRes):
        print("Success")
        exit()
    life -= 1
print("You lose")
```
