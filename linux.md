# LINUX COMMON HASHING 

## Algorithms 
		$1 = MD5 hashing algorithm.
		$2 =Blowfish Algorithm is in use.
		$2a= eksblowfish Algorithm
		$5 =SHA-256 Algorithm
		$6 =SHA-512 Algorithm
		
#### Examples 
 
        printf '%s' "mypasswd" | md5sum | cut -d ' ' -f 1
		32 chars : 3102125cae72c19f215480ddf2d0d5c3
		john --format=raw-md5
		
		printf '%s' "mypasswd" | sha256sum | cut -d ' ' -f 1
		64 chars : 0316001ef027cb1e25658d9faa50cb4c685223867f8a4d42b7994d817f0d2424
		john --format=raw-sha256

		printf '%s' "mypasswd" | sha512sum | cut -d ' ' -f 1
		128 chars : 1f5058b8002e14ed6bed143e7cf6f2846fa45c4f060e3415f19feac692338d6dd180b23732681d33319a3d450493b2f351cf8480b748013d665e9281acec0464
		john --format=raw-sha512

		
## crypt(3) 
$[hash-type]$[salt]$[passwd]
http://man7.org/linux/man-pages/man3/crypt.3.html

#### Examples 

http://php.net/manual/fr/function.crypt.php

    - DES 
 			$passwd = 'mypasswd'; 
 			$salt="rl";
			echo crypt($passwd,$salt);
			13 chars
			rlH586kzuP.N2
			john --format=des
	- MD5
			$passwd = 'mypasswd'; 
			$salt='$1$rasmusle$';
			echo crypt($passwd,$salt);
			33 chars
            $1$rasmusle$rLRf05zXyVzj2GeWu5XoH/
            john --format=md5crypt

	- SHA256
			$passwd = 'mypasswd'; 
			$salt='$5$rounds=5000$usesomesillystringforsalt$';
			echo crypt($passwd,$salt);
			 74 chars $5$rounds=5000$usesomesillystri$dnz6fovcglHKc1dISwy2BnwfMvVzafsdErtdRbLw8zD
            john --format=sha256crypt

	- SHA512
			$passwd = 'mypasswd'; 
			$salt='$6$rounds=5000$usesomesillystringforsalt$';
			echo crypt($passwd,$salt);
			117 chars : $6$rounds=5000$usesomesillystri$NsolLSC8R0oVwBdxzaxEauvnA1jtjDx6NTwZcz/pH9xHygGr6/m.77PDWFSPYSIHE8j.dy.BOMRMKW7zfkn3I/r
            john --format=sha521crypt

        
## bcrypt(1)

https://linux.die.net/man/1/bcrypt
        
#### Examples 

http://php.net/manual/fr/function.password-hash.php

        $passwd = 'mypasswd'; 
		$salt='$2a$07$usesomesillystringforsalt$';
		echo password_hash($passwd,PASSWORD_DEFAULT);
		$2y$10$JDJhJDA3JHVzZXNvbWVzaOSnUPeT9tfLPbjMHypSAxn8LDwHLfLrWr

		$passwd = 'mypasswd'; 
		$salt='$2a$07$usesomesillystringforsalt$';
		echo password_hash($passwd,PASSWORD_BCRYPT);
		$2y$10$JDJhJDA3JHVzZXNvbWVzaOSnUPeT9tfLPbjMHypSAxn8LDwHLfLrW
		
		john --format=bcrypt
        


 



