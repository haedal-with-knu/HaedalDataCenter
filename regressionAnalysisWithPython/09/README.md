# 09. 회귀모델의 실제 응용

9장은 이론적 설명 없이 선형모델을 사용해 해결된 실질적인 데이터 과학 문제의 네 가지 실제 예제로 구성됩니다.  
회귀문제, 불균형 및 다중 클래스 분류 문제, 순위 문제, 시계열 문제 중 회귀문제와 순위 문제를 정리하였습니다.  

* 데이터셋 다운로드

```python
pip install requests
```
```python
try:
    import urllib.request as urllib2
except:
    import urllib2

import requests, io, os
import zipfile, gzip

def download_from_UCI(UCI_url, dest):
    r = requests.get(UCI_url)
    filename = UCI_url.split('/')[-1]
    print ('Extracting in %s' % dest)
    try:
        os.mkdir(dest)
    except:
        pass
    with open (os.path.join(dest, filename), 'wb') as fh:
        print('\tdecompression %s' % filename)
        fh.write(r.content)
        
def unzip_from_UCI(UCI_url, dest):
    r = requests.get(UCI_url)
    z = zipfile.ZipFile(io.BytesIO(r.content))
    print ('Extracting in %s' % dest)
    
    for name in z.namelist():
        print ('\tunzipping %s' % name)
        z.extract(name, path=dest)

def gzip_from_UCi(UCI_url, dest):
    response = urllib2.urlopen(UCI_url)
    compressed_file = io.BytesIO(response.read())
    decompressed_file = gzip.GzipFile(fileobj=compessed_file)
    filename = UCI_url.split('/')[-1][:-4]
    print ('Extracting in %s' % dest)
    try:
        os.mkdir(dest)
    except:
        pass
    with open( os.path.join(dest, filename), 'wb') as outfile:
        print ('\tgunzipping %s' % filename)
        cnt = decompressed_file.read()
        outfile.write(cnt)
```
* 회귀문제 데이터셋 다운로드
