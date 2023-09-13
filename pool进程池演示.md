```python
from concurrent.futures import ThreadPoolExecutor
def tt(n):
    time.sleep(n)
    print('ok')
if __name__ == '__main__':
    with ThreadPoolExecutor(max_workers=5) as pool:
        for i in range(30):
            pool.submit(tt, 3)
```



