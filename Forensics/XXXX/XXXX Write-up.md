# XXXX Write-up


-----
### Category: Forensics

### Challenge Brief:

Is the flag hiding in plain sight?


-----


### Solution:

- The user is given a .pdf file which has the following text `The flag is xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`

- The user has to recover the flag from the .pdf file.

-----
To solve this one must understand the basic structure of a PDF file.

- The basic structure of a PDF file is composed of four parts.
  - Header 
  - Objects
  - Cross Reference Table
  - Trailer

A PDF reader always renders a PDF file from the end of the file. It reads the trailer first and follows the links in the cross reference table to the root object to build the logical structure of the document it is to render. 

If the reader encounters duplicate objects, it only takes into consideration what it encounters first and ignores any others.

- Viewing the PDF file with a PDF viewer we see:

```
The flag is xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

- Using a text editor like notepad to view the file allows you to see the structure of the file.

```
%PDF-1.1

1 0 obj
<<
 /Type /Catalog
 /Outlines 2 0 R
 /Pages 3 0 R
>>
endobj

2 0 obj
<<
 /Type /Outlines
 /Count 0
>>
endobj

3 0 obj
<<
 /Type /Pages
 /Kids [4 0 R]
 /Count 1
>>
endobj

4 0 obj
<<
 /Type /Page
 /Parent 3 0 R
 /MediaBox [0 0 612 792]
 /Contents 5 0 R
 /Resources <<
             /ProcSet [/PDF /Text]
             /Font << /F1 6 0 R >>
            >>
>>
endobj

5 0 obj
<<
 /Length 89
 /Filter /ASCII85Decode
>>
stream
6<#'\7PQ#@1a#b0+>GQ(+?(u.+B2ko-rakk+D,FuB-:o0+D#e>ASuR'@VfU_E+*Bj?Y!_h@rc:&FD5Z2?Z:%(FDkZ-CagK+C*5q;u~>
endstream
endobj

6 0 obj
<<
 /Type /Font
 /Subtype /Type1
 /Name /F1
 /BaseFont /Helvetica
 /Encoding /MacRomanEncoding
>>
endobj

xref
0 7
0000000000 65535 f
0000000012 00000 n
0000000089 00000 n
0000000145 00000 n
0000000214 00000 n
0000000419 00000 n
0000000594 00000 n
trailer
<<
 /Size 7
 /Root 1 0 R
>>
startxref
718
%%EOF

5 0 obj
<<
 /Length 89
 /Filter /ASCII85Decode
>>
stream
6<#'\7PQ#@1a#b0+>GQ(+?(u.+B2ko-rakk+D,FuB-:o0+F&-UG^+IXG^+IXG^+IXG^+IXG^+IXG^+IXG^+IXG^(Y[<,*OE;u~>
endstream
endobj

xref
0 1
0000000000 65535 f
5 1
0000000935 00000 n
trailer
<<
 /Size 7
 /Root 1 0 R
 /Prev 718
>>
startxref
1110
%%EOF

```

- Notice that there are two trailers, xref/cross reference tables and two object 5's as well.
- On removing the duplicates your file should look like this:

```
%PDF-1.1

1 0 obj
<<
 /Type /Catalog
 /Outlines 2 0 R
 /Pages 3 0 R
>>
endobj

2 0 obj
<<
 /Type /Outlines
 /Count 0
>>
endobj

3 0 obj
<<
 /Type /Pages
 /Kids [4 0 R]
 /Count 1
>>
endobj

4 0 obj
<<
 /Type /Page
 /Parent 3 0 R
 /MediaBox [0 0 612 792]
 /Contents 5 0 R
 /Resources <<
             /ProcSet [/PDF /Text]
             /Font << /F1 6 0 R >>
            >>
>>
endobj

5 0 obj
<<
 /Length 89
 /Filter /ASCII85Decode
>>
stream
6<#'\7PQ#@1a#b0+>GQ(+?(u.+B2ko-rakk+D,FuB-:o0+D#e>ASuR'@VfU_E+*Bj?Y!_h@rc:&FD5Z2?Z:%(FDkZ-CagK+C*5q;u~>
endstream
endobj

6 0 obj
<<
 /Type /Font
 /Subtype /Type1
 /Name /F1
 /BaseFont /Helvetica
 /Encoding /MacRomanEncoding
>>
endobj

xref
0 7
0000000000 65535 f
0000000012 00000 n
0000000089 00000 n
0000000145 00000 n
0000000214 00000 n
0000000419 00000 n
0000000594 00000 n
trailer
<<
 /Size 7
 /Root 1 0 R
>>
startxref
718
%%EOF

```

Save the file and open it with a PDF reader to see:

```
Flag is HilltopCTF{xtra_trail3r_xref}
```

The flag is `HilltopCTF{xtra_trail3r_xref}`