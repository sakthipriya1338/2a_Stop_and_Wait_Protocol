# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM:

##CLIENT:

# Developed By : SAKTHIPRIYA R
# Register Number : 212225220088
import socket

HOST = 'localhost'
PORT = 8000

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    try:
        s.bind((HOST, PORT))
    except OSError as exc:
        print(f"Port {PORT} busy: {exc}. Trying an available port.")
        s.bind((HOST, 0))
        PORT = s.getsockname()[1]
        print(f"Server bound to {HOST}:{PORT} instead.")

    s.listen(5)
    print(f"Listening on {HOST}:{PORT}...")
    c, addr = s.accept()
    print('Connected by', addr)
    with c:
        while True:
            message = input("Enter a data: ")
            if not message:
                print("No data entered. Closing connection.")
                break
            c.send(message.encode())
            ack = c.recv(1024).decode()
            if ack:
                print("Client says:", ack)
            else:
                print("Client closed the connection.")
                break
##SERVER:

import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    print(s.recv(1024).decode())
    s.send("Acknowledgement Recived".encode())
## OUTPUT:
<img width="1630" height="1014" alt="Screenshot 2026-05-22 110552" src="https://github.com/user-attachments/assets/0df08f13-3db1-43d7-950a-3e148dcf5bff" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
