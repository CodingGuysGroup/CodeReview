## `문제 설명`
전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.

전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

### `제한 사항`
phone_book의 길이는 1 이상 1,000,000 이하입니다.

각 전화번호의 길이는 1 이상 20 이하입니다.

같은 전화번호가 중복해서 들어있지 않습니다.

### `입출력 예제`


|phone_book|return|
|---|---|
|["119", "97674223", "1195524421"]|false|
|["123","456","789"]|	true|
|["12","123","1235","567","88"]|false|

### `입출력 예 설명`
- 입출력 예 #1
앞에서 설명한 예와 같습니다.

- 입출력 예 #2
한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 true입니다.

- 입출력 예 #3
첫 번째 전화번호, “12”가 두 번째 전화번호 “123”의 접두사입니다. 따라서 답은 false입니다.
---
## 'Explanation of the problem'
I want to check if one of the phone numbers in the phone book is a prefix for another number.

If the phone number is as follows, the rescue team phone number is the prefix of Youngseok's phone number.

- Rescue team: 119
- Park Joonyoung: 97674223
- Ji Young-seok: 1195524421

When an array of phone_books containing phone numbers in the phone book is given as a parameter of the solution function, write a solution function to return false if one number is a prefix of another number, or true if not.

### 'Restrictions'
The length of the phone_book is greater than or equal to 1 and less than or equal to 1,000,000.

The length of each phone number is 1 or more and 20 or less.

The same phone number does not contain duplicate numbers.

### 'Example Input/Output'


|phone_book|return|
|---|---|
|["119", "97674223", "1195524421"]|false|
|["123","456","789"]|	true|
|["12","123","1235","567","88"]|false|

### 'Example Input/Output'
- Input/Output Example #1
Same as the previous example.

- Input/Output Example #2
Since one number is never a prefix to another number, the answer is true.

- Input/Output Example #3
The first phone number, "12", is the prefix for the second phone number, "123". So the answer is false.

---
## `ANS`
```python
def solution(phone_book):
    answer = True
    
    for i in range(len(phone_book)):
        for j in range(i+1, len(phone_book)):
            if phone_book[j].find(phone_book[i]) == 0 or phone_book[i].find(phone_book[j]) == 0:
                answer = False
                break
    
    return answer
```    
![image](https://user-images.githubusercontent.com/86946575/226539125-7eb823a6-b4fc-4de5-9bf9-0cd8c0c03bcb.png)
### `효울성 좋은것`
```python
def solution(phoneBook):
    phoneBook = sorted(phoneBook)

    for p1, p2 in zip(phoneBook, phoneBook[1:]):
        if p2.startswith(p1):
            return False
    return True
```

### Feedback
---
#### 상우
1. find 함수를 잘 사용하여 간단하게 구현한 것이 인상적이나 find함수는 리스트에서 O(N)의 시간복잡도를 갖기 때문에 worst case 경우 O(N^3)의 시간복잡도를 갖을 수 있을 것으로 보임
2. zip,startswith 함수를 이용하여 for문을 하나로 처리하고 효율성을 높인 것이 인상적임

#### 수빈
1. 해시(dictionary)를 사용하지 않고 주어진 배열을 통해서 문제의 답을 도출해낸 것이 인상적이다.
2. 효율성면에서 zip과 startswith를 사용하여 풀이한 것 또한 새로운 함수를 배워가는 좋은 기회라고 생각한다.


