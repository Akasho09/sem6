## User wants to retrieve an EBCDIC file named file1 from /usr/usrs/report directory on host mcGraw.com. The file is large, so it should be compressed before transfer.

ftp mcGraw.com              // Connect to FTP server
Name: anonymous             // Login as anonymous or provide username
Password: <enter password>  // Enter password

cd /usr/usrs/report         // Navigate to the correct directory
type E                     // Set transfer type to EBCDIC
quote MODE Z               // Request compression (MODE Z is used for compression if supported)
get file1                  // Download the compressed EBCDIC file
bye                        // Close the connection

or
---
🛠️ FTP Commands and Responses

ftp mcGraw.com
Response:
Connected to mcGraw.com.
220 FTP Server Ready.

Name (mcGraw.com:your_username): your_username
Response:
331 Password required for your_username.

Password: your_password
Response:
230 User your_username logged in.

cd /usr/usrs/report
Response:
250 Directory changed to /usr/usrs/report.

type E
Response:
200 Type set to EBCDIC.

mode C
Response:
200 Mode set to Compressed.

get file1
Response:
150 Opening data connection for file1 (compressed).
226 Transfer complete.

bye
Response:
221 Goodbye.


## Assume there is a server with the domain name www.uncommon.com
i) Show a request that asks for information about a document at /bin/users/file. Use at least two general headers and one request header.
ii) Show the response to part (i) for a successful reques

i) HTTP Request:
GET /bin/users/file HTTP/1.1
Host: www.uncommon.com
User-Agent: Mozilla/5.0
Accept: text/plain

Explanation of Headers:
1. General Headers:
Host: Specifies the domain name of the server (required in HTTP/1.1).
User-Agent: Identifies the client software initiating the request.

2. Request Header:
Accept: Informs the server about the types of media that the client can process. Here, it indicates that the client prefers plain text.

ii) HTTP Response (for successful request):
HTTP/1.1 200 OK
Date: Thu, 08 May 2025 17:00:00 GMT
Server: Apache/2.4.41 (Unix)
Content-Type: text/plain
Content-Length: 348
Last-Modified: Wed, 07 May 2025 14:30:00 GMT
Connection: close

[... contents of file ...]


## File Transfer from /usr/usrs/report to /usr/usrs/letters
put file1.Z /usr/usrs/letters/file1.Z

- to compress the file
cd /usr/usrs/report
!compress file1

- set compress mode 
mode C
get file1
