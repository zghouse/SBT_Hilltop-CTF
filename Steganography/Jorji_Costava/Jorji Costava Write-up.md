# Jorji Costava Write-up


-----
### Category: Steganography

### Challenge Brief:

In the light of recent terrorist attacks, Arstotzka has closed off it's borders. Jorji needs to get into Arstotzka as he has very important business to tend to. Luckily Jorji has a friend at the border patrol who has managed to get Jorji a pre-approved passport number. Jorji has received an email with a .pdf file from his friend which contains the password. Jorji is no good with computers. Can you help Jorji find the passport number he needs to get his passport made?


-----


### Solution:

- The user is given a .pdf file. 

- The user has to help Jorji recover a pre-approved passport number, which Jorji's friend at the border patrol has hidden in the .pdf file.


-----
The user can achieve this by using a pdf parser to parse the given file. 
Didier Stevens `pdf-parser` comes pre-installed in Kali. Parsing the given file using `pdf-parser` will give you the pre-approved passport number Jorji needs, which in this case is the flag.

```
pdf-parser.py Flyer.pdf | less
```
The flag is `HilltopCTF{AW4QS-GUXM9}`