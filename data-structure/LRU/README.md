# LRU (Least Recently Used Algorithm)

> [참고링크 강생강의 하루](https://gingerkang.tistory.com/26)

## 개념
- 페이지 교체 알고리즘의 종류 중 하나
- 가장 오랫동안 사용되지 않은 페이지를 제거하는 알고리즘

## 코드
```python
cacheSize = 3
reference = [4, 2, 3, 4, 5, 6, 5, 4, 7]
cache = []
for ref in reference:
  if not ref in cache:
    if len(cache) < cacheSize:
        cache.append(ref)
     else:
        cache.pop(0)
        cache.append(ref)
  else:
    cache.pop(cache.index(ref))
    cache.append(ref)
```