# **CTF Writeup —** Nom Nom Nom (stegnography)

# **Step 1: Metadata Extraction**

Running `exiftool` on the provided image revealed a suspicious field:

`exiftool old_photo.jpg`

`UserComment: Rk1ZU01MQ0FOQjVXWTJKRU9aU0hZNVJFTk5XRUU9PT0=`

The trailing `==` strongly indicated **Base64** encoding.

## **Step 2: Base64 Decoding**

Decoded using:

`echo "Rk1ZU01MQ0FOQjVXWTJKRU9aU0hZNVJFTk5XRUU9PT0=" | base64 -d`

Result:

`FMYSMLCANB5WY2JEOZSHY5RENNWEE==`

This format (A–Z \+ 2–7 \+ padding \== ) corresponds to **Base32**.

## **Step 3: Base32 Decoding**

Decoded using:

`echo "FMYSMLCANB5WY2JEOZSHY5RENNWEE==" | base32 -d`

Result:    

`+1&,@h{li$vd|v$klB`

Still not a readable flag → clearly another layer of encoding.

## **Step 4: ASCII Shift Cipher Decoding**

The string appeared obfuscated with a **custom ASCII Shift Cipher**.  
 After analyzing character patterns, the following transformation was derived:

* Characters at indices **0,1,2,3,4,9,14,17** → `ord(char) + 59`

* All other characters → `ord(char) - 35`

* Applying this transformation revealed the hidden flag.

### **Example Mapping**

`'+' (index 0)  → ord('+') + 59 = 'f'`  
`'1' (index 1)  → ord('1') + 59 = 'l'`  
`'&' (index 2)  → ord('&') + 59 = 'a'`  
`',' (index 3)  → ord(',') + 59 = 'g'`  
`'@' (index 4)  → ord('@') + 59 = '{'`  
`...`

Final result after processing the entire string:

`flag{EXIF_SAYS_HI}`

## **Final Flag**

`flag{EXIF_SAYS_HI}`  
