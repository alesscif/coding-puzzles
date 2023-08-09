---
description: https://leetcode.com/problems/read-n-characters-given-read4/
---

# 157. Read N Characters Given Read4

Given a `file` and assume that you can only read the file using a given method `read4`, implement a method to read `n` characters.

**Method read4:**

The API `read4` reads **four consecutive characters** from `file`, then writes those characters into the buffer array `buf4`.

The return value is the number of actual characters read.

#### Solution:

\
Translating the description into English is the hardest part here. Essentially, we're given a method which can only read characters in groups of four. The question is "how do we use a method that reads four things at a time to read any number of things?". Answer is simple:&#x20;

* initialize a counter to keep track of how many characters we've read so far:

```
int readCount = 0;
```

* for each group of four characters in n, initialize a buf4 array, read to it by calling read4(buf4), and store the number of actually read characters (which may be smaller than 4)

```
for (int i = 0; i < n; i+=4) {    
    char[] buf4 = new char[4]; 
    int read4Count = read4(buf4);
    //
}
```

* since we now have access to all the characters read to the buf4 array, all that's left is copying them over to our own buf array, making sure we stop copying if we've copied all the characters read to buf4 (read4Count) or enough total characters to reach n total characters (our target)

```java
public int read(char[] buf, int n) {
    int readCount = 0;
    for (int i = 0; i < n; i+=4) {    
        char[] buf4 = new char[4]; 
        int read4Count = read4(buf4);
        for (int j = 0; j < read4Count && readCount < n; j++) {
            buf[i+j] = buf4[j];
            readCount++;
        }
    }
    return readCount;
}
```
