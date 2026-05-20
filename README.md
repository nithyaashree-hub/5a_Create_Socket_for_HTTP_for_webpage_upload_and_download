# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
#
Server
```
import socket

s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("index.html","a")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```
Client
```
import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1-Download 2-Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```
## OUTPUT
Download 

<img width="1302" height="227" alt="image" src="https://github.com/user-attachments/assets/8f4c716d-c9de-406c-a2a8-29d76436fce5" />

Upload

<img width="1322" height="211" alt="image" src="https://github.com/user-attachments/assets/ddfe0e7f-3fcf-4b0f-8241-3775c64bffb4" />

After uploading

<img width="400" height="191" alt="image" src="https://github.com/user-attachments/assets/a80c4364-9d71-4eb0-9fc4-6f3457fad45b" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
