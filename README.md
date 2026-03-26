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
### client
```python
import socket

HOST = '127.0.0.1'
PORT = 8080

client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect((HOST, PORT))

choice = input("Enter 1 for GET (Download), 2 for POST (Upload): ")

if choice == "1":
    request = "GET / HTTP/1.1\r\nHost: localhost\r\n\r\n"
elif choice == "2":
    data = input("Enter data to upload: ")
    request = f"POST / HTTP/1.1\r\nHost: localhost\r\nContent-Length: {len(data)}\r\n\r\n{data}"

client_socket.send(request.encode())

response = client_socket.recv(4096).decode()
print("Response from server:\n", response)

client_socket.close()
```
### server
```python
import socket

HOST = '127.0.0.1'
PORT = 8080

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind((HOST, PORT))
server_socket.listen(1)

print("Server running at http://127.0.0.1:8080")

while True:
    client_socket, addr = server_socket.accept()
    print("Connected by", addr)

    request = client_socket.recv(1024).decode()
    print("Request:\n", request)

    if "GET" in request:
        try:
            with open("index.html", "r") as file:
                content = file.read()
            response = "HTTP/1.1 200 OK\n\n" + content
        except:
            response = "HTTP/1.1 404 Not Found\n\nFile not found"

        client_socket.sendall(response.encode())

    elif "POST" in request:
        data = request.split("\r\n\r\n")[1]
        with open("uploaded.txt", "w") as file:
            file.write(data)

        response = "HTTP/1.1 200 OK\n\nData uploaded successfully"
        client_socket.sendall(response.encode())

    client_socket.close()

```
## OUTPUT
### CLIENT:

<img width="1204" height="347" alt="image" src="https://github.com/user-attachments/assets/e346b021-b8b2-422c-bb7f-b1ab52cf3611" />

### SERVER:

<img width="1214" height="141" alt="image" src="https://github.com/user-attachments/assets/2e7f1079-a4a9-49a1-b540-3618135f5239" />



## Result
Thus the socket for HTTP for web page upload and download created and Executed

