# Assignment on Regular Expressions

?> <i class="fa-solid fa-circle-info"></i> http://www.regular-expressions.info/

## Task 1
Create the file regtest.txt with the following content:

```
apple
banana
apricot
pear
peach
strawberry
mango
grape
orange
5isanumber
123
123abc
abc123
35abcd35
5five5
55fivefive55
555fivefivefive555
77sevenseven77
@d
@tsign@@
atsiiiiiiiiiiiign
```

## Task 2
Use regular expressions to filter the lines that:

1.	Contain the letter a
```
   Output:
      apple
      banana
      apricot
      peach
      strawberry
      mango
      grape
      orange
      5isanumber
      123abc
      abc123
      35abcd35
      atsiiiiiiiiiiiign
```  	
2.	Contain the letter a or s
```
   Output:
      apple
      banana
      apricot
      peach
      strawberry
      mango
      grape
      orange
      5isanumber
      123abc
      abc123
      35abcd35
      77sevenseven77
      @tsign@@
      atsiiiiiiiiiiiign
``` 
3.	Contain the letter a and s
```
   Output:
      strawberry
      5isanumber
      atsiiiiiiiiiiiign
``` 
4.	Contain a @
```
   Output:
      @d
      @tsign@@   
``` 
5.	Start with the letter p
```
   Output:
      peer
      peach
``` 
6.	End with the letter t 
```
   Output:
      apricot
``` 
7.	Start with a number 
```
   Output:
      5isanumber
      123
      123abc
      35abcd35
      5five5
      55fivefive55
      555fivefivefive555
      77sevenseven77
``` 
8.	Start with a number and end with a letter 
```
   Output:
      5isanumber
      123abc
``` 
9.	Contains 2 or more consecutive letters i
```
   Output:
      atsiiiiiiiiiiiign
``` 
10.	Only contains numbers
```
   Output:
      123
``` 
11.	Only contains letters
```
   Output:
      apple
      banana
      apricot
      peer
      peach
      strawberry
      mango
      grape
      orange
      atsiiiiiiiiiiiign
``` 
12.	Contains one or more numbers, followed by one or more letters
```
   Output:
      5isanumber
      123abc
      35abcd35
      5five5
      55fivefive55
      555fivefivefive555
      77sevenseven77
``` 
13.	Contains one or more numbers, followed by one or more letters and ending with a number. 
```
   Output:
      5five5
``` 


## Task 3
Use sed to: 

1.	create a file regtest_5.txt from the file regtest.txt where all numbers 5 are replaced with "five"
2.	create a file regtest_7.txt from the file regtest.txt where the text ‘seven’ is replaced by the number 7
3.	create a file regtest_at.txt from the file regtest.txt where all the @ symbols are replaced by _at_


## Task 4
Count the amount of time 5 can be found in regtest.txt
search the manpage of grep for a solution

## Task 5
Search in the bash manpage to the header named "REDIRECTION" (The text starts at the left-side line). Is this search-function case sensitive? 

## Task 6
Try with the same regular expression to only show hidden files from your home folder. 
  
## Task 7
Use the command `ls -la ~` and change in the output: 

?> <i class="fa-solid fa-circle-info"></i> The reference "." To ". (this folder)" and ".." to ".. (parent folder)". Also remove the line that shows the amount of files and folders in the directory   
  
?> <i class="fa-solid fa-circle-info"></i> Hint: if you use the $ sign at the end of a string to search, it means the line needs to end with that string.   
To complete this task you will have to use the `sed` command multiple times
