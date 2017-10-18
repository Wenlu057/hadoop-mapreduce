### IO— Core tools for working with streams

The io module provides Python’s main facilities for dealing with various types of I/O. There are three main types of I/O: text I/O, binary I/O and raw I/O. A concrete object belonging to any of these categories is called a **file object**. Other common terms are stream and **file-like object**.

* **Text I/O**

The easiest way to create a text stream is with open(), optionally specifying an encoding:


```
f = open("myfile.txt", "r", encoding="utf-8")
```

In-memory text streams are also available as StringIO objects:


```
f = io.StringIO("some initial text data")
```

* **Binary I/O**

The easiest way to create a binary stream is with open() with 'b' in the mode string:


```
f = open("myfile.jpg", "rb")
```


**StringIO**

An in-memory stream for text I/O. The text buffer is discarded when the close() method is called.

### Python Built-in Types
**Text Sequence Type-str**



```
str.strip([chars])
```
Return a copy of the string with the leading and trailing characters removed. The chars argument is a string specifying the set of characters to be removed. If omitted or None, the chars argument defaults to removing whitespace.



```
>>> '   spacious   '.strip()
'spacious'
>>> 'www.example.com'.strip('cmowz.')
'example'
```


