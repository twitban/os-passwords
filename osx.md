# ALGORITHM 

Creating ShadowHashData (valid in OS 10.8 and newer)

- PRF is a pseudorandom function of two parameters with output length hLen (e.g. a keyed HMAC)
- Password is the master password from which a derived key is generated
- Salt is a sequence of bits, known as a cryptographic salt
- c is the number of iterations desired
- dkLen is the desired length of the derived key

to create DK = PBKDF2(PRF, Password, Salt, c, dkLen)

https://apple.stackexchange.com/questions/220729/what-type-of-hash-are-a-macs-password-stored-in

## GET THE FILES

https://www.onlinehashcrack.com/how-to-extract-hashes-crack-mac-osx-passwords.php

#### Location : 

        var/db/dslocal/nodes/Default/users/<username>.plist
        sudo dscl . read /Users/%user% AuthenticationAuthority
        sudo dscl . read /Users/%user% dsAttrTypeNative:ShadowHashData

### First method :  auto & simple 

https://github.com/octomagon/davegrohl

### Second method : manually 

- Get he Hash 

        sudo defaults read /var/db/dslocal/nodes/Default/users/user.plist ShadowHashData

- Remove everything excepts the hex 

        sudo defaults read /var/db/dslocal/nodes/Default/users/user.plist ShadowHashData | tr -dc 0-9a-f

- Revert hex to (malformed) binary 

        sudo defaults read /var/db/dslocal/nodes/Default/users/user.plist ShadowHashData | tr -dc 0-9a-f | xxd -r -p$ml$<iterations(integer)>$<salt(hex)>$<entropy(hex)>

- Finally convert ot xml file 

        sudo defaults read /var/db/dslocal/nodes/Default/users/user.plist ShadowHashData | tr -dc 0-9a-f | xxd -r -p  | plutil -convert xml1 - -o ~/Desktop/tempuser.plist

The plist contains three key parts: iterations, entropy and salt.
iterations is just an integer, but entropy and salt are base64 encoded. To continue working with them you have to decode and xxd them:

- Decode salt 

        echo  "salt_data" | base64 -D | xxd -p | tr -d \\n > salt

- Decode entropy with the same  

        echo  "entropy" | base64 -D | xxd -p | tr -d \\n > entropy

- Combine them to prepare hashcat file 

        $ml$<iterations(integer)>$<salt(hex)>$<entropy(hex)>
        

john --format=PBDKF2-HMAC-SHA512./mac-hash.txt 
