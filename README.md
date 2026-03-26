# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm
### Client Side (Browser-like)

1.Start the program

2.Create a socket using TCP

3.Connect to the server using IP address and port

4.Send HTTP request (GET for download / POST for upload)

5.Receive response from server

6.Display or save the webpage content

7.Close the connection

8.Stop the program

### Server Side

1.Start the program

2.Create a socket using TCP

3.Bind the socket to an IP address and port

4.Listen for incoming connections

5.Accept client request

6.Read HTTP request (GET/POST)

7.If GET → send webpage content

8.If POST → receive uploaded data and store it

9.Send HTTP response to client

10.Close connection

11.Stop the program

## Program 
client
```
import socket
s=socket.socket()
s.connect(("localhost",8080))
ch=input("1.Download 2.Upload : ")
if ch=="1":
    s.send("GET / HTTP/1.1\nHost: localhost\n\n".encode())
    print(s.recv(4096).decode())
else:
    msg=input("Enter data to upload: ")
    s.send(("POST / HTTP/1.1\nHost: localhost\n\n"+msg).encode())
    print(s.recv(1024).decode())
s.close()
```

server
```
import socket
s=socket.socket()
s.bind(("localhost",8080))
s.listen(1)
print("Server running...")
while True:
    c,addr=s.accept()
    req=c.recv(1024).decode()
    print("Request received")
    if "GET" in req:
        f=open("index.html","r")
        res="HTTP/1.1 200 OK\n\n"+f.read()
        f.close()
        c.send(res.encode())
    elif "POST" in req:
        data=req.split("\n\n")[1]
        f=open("upload.txt","w")
        f.write(data)
        f.close()
        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())
    c.close()

```
## OUTPUT

<img width="997" height="332" alt="image" src="https://github.com/user-attachments/assets/035a0730-9cce-4071-85d0-288d484493d7" />

<img width="529" height="181" alt="image" src="https://github.com/user-attachments/assets/7b9d3c57-d115-4b8a-ab61-161c4eff3efd" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed

