# Recursively-Remove-all-Adjacent-Duplicate-Characters-in-Python

Remove all Adjacent Duplicate Characters Recursively in Python
Here, on this page, we will learn how to write the program to Remove all Adjacent Duplicate Characters Recursively in Python. programming language. After removing all its adjacent duplicate characters, we are given a string and need to return the string.

Example :

Input : str = “acaabbbceddd”
Output : ae
Remove all Adjacent Duplicate Characters Recursively

Method Discussed :
Method 1 : Using Recursive Way
Method 2 : Using  Non-Recursive Way
Method 1:
In this algorithm, we will discuss the recursive way to remove all duplicate characters from the given input string s.

First we check whether the String remStr has the repeated character that matches the last char of the parent String.
If that is so then we have to keep removing that character before concatenating string s and string remStr.
Remove all Adjacent Duplicate Characters Recursively in Python
Python Code
Run
def removeUtil(string, last_removed):

    if len(string) == 0 or len(string) == 1:
        return string

    if string[0] == string[1]:
        last_removed = ord(string[0])

        while len(string) > 1 and string[0] == string[1]:
            string = string[1:]

        string = string[1:]
        return removeUtil(string, last_removed)

    rem_str = removeUtil(string[1:], last_removed)

    if len(rem_str) != 0 and rem_str[0] == string[0]:
        last_removed = ord(string[0])
        return rem_str[1:]

    if len(rem_str) == 0 and last_removed == ord(string[0]):
        return rem_str

    return [string[0]] + rem_str


def remove(string):
    last_removed = 0
    return "".join(removeUtil(list(string), last_removed))


string1 = "acaabbbceddd"
print(remove(string1))
Output
ae
Method 2:
In this method, we will check whether the String remStr has the repeated character that matches the last char of the parent String. If that is happening then we have to keep removing that character before concatenating string s and string remStr.

Run
def removeDuplicates(s, ch):
    if s is None or len(s) <= 1:
        return s

    i, j = 0, 0
    while i < len(s):

        if i + 1 < len(s) and s[i] == s[i + 1]:
            j = i

            while j + 1 < len(s) and s[j] == s[j + 1]:
                j += 1

            if i > 0:
                lastChar = s[i - 1]
            else:
                lastChar = ch

            remStr = removeDuplicates(s[j + 1:], lastChar)

            s = s[0: i]

            while len(remStr) > 0 and len(s) > 0 and remStr[0] == s[len(s) - 1]:

                while len(remStr) > 0 and remStr[0] != ch and remStr[0] == s[len(s) - 1]:
                    remStr = remStr[1: len(remStr)]

                s = s[0: len(s) - 1]

            s = s + remStr
            i = j

        else:
            i += 1

    return s


str1 = "mississipie"
print(removeDuplicates(str1, ' '))
Output
mpie
