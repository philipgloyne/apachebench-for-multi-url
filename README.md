## Apachebench-for-multi-url

Mirror for http://code.google.com/p/apachebench-for-multi-url/ with 'random url' fix listed here http://code.google.com/p/apachebench-for-multi-url/issues/detail?id=1

### Description

Multiple URL requests for ApacheBench. You can set URL list with '-L filename'.


### Compile ab-multi with random url patch

```
gcc -I /usr/include/apr-1.0 -I /usr/include/apache2 ab.c -o ab  -lm -lapr-1 -laprutil-1
```

### Build Instructions (Linux)
```
git checkout https://github.com/philipgloyne/apachebench-for-multi-url.git
docker run -ti --rm -v `pwd`/apachebench-for-multi-url:/build alpine /bin/sh
apk add build-base apr-util-dev apache2-dev openssl-libs-static
cd /build
gcc -I /usr/include/apr-1 -I /usr/include/apache2 -I /usr/include/openssl ab.c -o ab -lm -lapr-1 -laprutil-1 -lssl -lcrypto -ldl -static
```

### Example Usage

```
ab -c 100 -v 4 -n 2000 -L urls.txt > results.txt
```

### Known Bugs

The first URL selected per concurrent user (-c 100 - above example) will always be the first URL in the supplied file (-L urls.txt). Every subsequent URL selected will be random. So in the above example the first url will be called 100 times concurrently, then 1900 random urls will be selected from the file urls.txt. A fork fix would be appreciated.

### Credit

All Credit goes to 
- craqueez@gmail.com
- bhartshorne@wikimedia.org
- https://github.com/Popolon
- https://github.com/rsubr

### Code License

Apache License 2.0
