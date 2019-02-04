# ALGORITHM 

## LM 
(Vista / Server 2008)
1. Convert all lower case to upper case
2. Pad password to 14 characters with NULL characters
3. Split the password to two 7 character chunks
4. Create two DES keys from each 7 character chunk
5. DES encrypt the string "KGS!@#$%" with these two chunks
6. Concatenate the two DES encrypted strings. This is the LM hash 

        john --format=lm hash.txt
        hashcat -m 3000 -a 3 hash.txt

 ## NT

MD4(UTF-16-LE(password))

        john --format=nt hash.txt
		hashcat -m 1000 -a 3 hash.txt


## GET THE FILES

As Administrator run :
        
#### First method  save register 
        reg save hklm\sam c:\sam
        reg save hklm\system c:\system
        sampdump2 system sam out.txt

#### Second method boot on usb debian/kali 
    mkdir /mnt/win
    fdisk -l 
    umount /dev/sd[widwos disk]
    mount remove_hiberfile /dev/sd[windows disk] /mnt/win
    cp /mnt/win/C:/windows/system32/sam ./
    cp /mnt/win/C:/windows/system32/system ./
    sampdump2 system sam out.txt
    
    
    john --format=NT out.txt SUCKS 
    
        
