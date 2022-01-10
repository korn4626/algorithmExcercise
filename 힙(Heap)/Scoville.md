# [더맵게][link]
[https://programmers.co.kr/learn/courses/30/lessons/42626][link]
## 문제설명
매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 
모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.
```
섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
```

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

## 제한사항
- scoville의 길이는 2 이상 1,000,000 이하입니다.
- K는 0 이상 1,000,000,000 이하입니다.
- scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.


## 입출력 예
<table class="table">
        <thead><tr>
<th>scoville</th>
<th>K</th>
<th>return</th>
</tr>
</thead>
        <tbody><tr>
<td>[1, 2, 3, 9, 10, 12]</td>
<td>7</td>
<td>2</td>
</tr>
</tbody>
      </table>

## 입출력 예 설명
1. 스코빌 지수가 1인 음식과 2인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
새로운 음식의 스코빌 지수 = 1 + (2 * 2) = 5
가진 음식의 스코빌 지수 = [5, 3, 9, 10, 12]

2. 스코빌 지수가 3인 음식과 5인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
새로운 음식의 스코빌 지수 = 3 + (5 * 2) = 13
가진 음식의 스코빌 지수 = [13, 9, 10, 12]

모든 음식의 스코빌 지수가 7 이상이 되었고 이때 섞은 횟수는 2회입니다.

## 풀이
```python
import heapq
def solution(scoville, K):
    answer = 0
    
    #heapq.heappop -> 은 pop한후에 정렬이 되기 떄문에...(엄밀히 말하면 최소값이 아닌 0번째를 갖고 온후 heap 구현)
    #미리 sort를 하거나...
    #heapq.heapify(scoville) 해야함.
    
    scoville.sort()
    while len(scoville) > 1:
        k = heapq.heappop(scoville)
        if k > K:
            break
        tmp = heapq.heappop(scoville)
        heapq.heappush(scoville, k + (tmp * 2))
        answer += 1
    if scoville and heapq.heappop(scoville) <= K:
        answer = -1
    return answer
```

## 결과
정확성  테스트
```
테스트 1 〉	통과 (0.00ms, 10.2MB)
테스트 2 〉	통과 (0.00ms, 10.2MB)
테스트 3 〉	통과 (0.01ms, 10.2MB)
테스트 4 〉	통과 (0.01ms, 10.2MB)
테스트 5 〉	통과 (0.01ms, 10.2MB)
테스트 6 〉	통과 (0.47ms, 10.2MB)
테스트 7 〉	통과 (0.37ms, 10.2MB)
테스트 8 〉	통과 (0.05ms, 10.2MB)
테스트 9 〉	통과 (0.04ms, 10.2MB)
테스트 10 〉	통과 (0.32ms, 10.2MB)
테스트 11 〉	통과 (0.20ms, 10.3MB)
테스트 12 〉	통과 (0.73ms, 10.3MB)
테스트 13 〉	통과 (0.40ms, 10.2MB)
테스트 14 〉	통과 (0.01ms, 10.2MB)
테스트 15 〉	통과 (0.49ms, 10.2MB)
테스트 16 〉	통과 (0.00ms, 10.2MB)
```
효율성 테스트
```
테스트 1 〉	통과 (172.56ms, 16.1MB)
테스트 2 〉	통과 (374.22ms, 22MB)
테스트 3 〉	통과 (1522.82ms, 49.7MB)
테스트 4 〉	통과 (125.43ms, 14.9MB)
테스트 5 〉	통과 (1630.82ms, 51.8MB)
```
채점 결과
```
정확성: 76.2
효율성: 23.8
합계: 100.0 / 100.0
```
[link]:https://programmers.co.kr/learn/courses/30/lessons/42626
