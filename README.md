# Chat Application

A real-time multi-room chat application built with Python, featuring a server with admin controls and a client GUI.

## Features

### Server
- **Multi-room Support**: Create and manage multiple chat rooms simultaneously
- **Room Security**: Password-protected rooms
- **Admin Controls**:
  - Kick users from rooms
  - Close entire rooms
  - Monitor active rooms and users
- **Real-time Monitoring**: Live view of all active rooms and participants
- **Graceful Shutdown**: Properly notifies clients before server termination

### Client
- **Room Management**: Create new rooms or join existing ones
- **Nickname System**: Unique nicknames per room
- **Real-time Messaging**: Instant message delivery to all room participants
- **User-Friendly Interface**: Clean GUI for easy navigation
- **Connection Handling**: Proper error handling and reconnection prompts

## Installation

1. Install required dependencies:
```bash
pip install PyQt5
```

## Usage

### Starting the Server

1. Run the server application:
```bash
python server.py
```

2. Configure the server host and port in the code if needed (default: 192.168.1.10:1111)

3. Use the server admin interface to:
   - Start/stop the server
   - Monitor active rooms
   - Manage users (kick)
   - Close rooms

### Using the Client

1. Run the client application:
```bash
python client.py
```

2. In the start window:
   - Enter a room ID
   - Provide the room password
   - Choose your nickname
   - Click "Create Room" or "Join Room"

3. In the chat window:
   - Type messages in the input field
   - Press Enter or click "Send" to send messages
   - Click "Leave Room" to exit the current room

## Protocol Details

### Client-Server Communication

The application uses a custom protocol over TCP sockets:

1. **Connection Initialization**:
   - Server sends "ROOM" to request room details
   - Client responds with "ACTION:ROOM_ID:PASSWORD" (CREATE or JOIN)
   - Server validates and responds with status codes

2. **Nickname Assignment**:
   - Server sends "NICK" to request nickname
   - Client responds with chosen nickname

3. **Message Format**:
   - Regular messages: "NICKNAME: message content"
   - System messages: Prefixed with server notifications
   - Special commands: "LEAVE_ROOM" to exit gracefully

### Status Codes

- "ROOM_EXISTS": Room ID already taken
- "NO_SUCH_ROOM": Room doesn't exist
- "WRONG_PASSWORD": Incorrect password
- "NICKNAME_TAKEN": Nickname already in use in the room
- "INVALID_REQUEST": Malformed request

## Configuration

### Server Settings
Modify these constants in the server code:
```python
HOST = '192.168.1.10'  # Server IP address
PORT = 1111            # Server port
```

### Network Requirements
- Server must be accessible to all clients
- Firewall should allow traffic on the specified port
- For LAN usage, ensure all devices are on the same network

## Troubleshooting

### Common Issues

1. **Connection Refused**
   - Ensure server is running
   - Verify host and port settings match between server and clients
   - Check firewall settings

2. **Room Creation/Join Fails**
   - Verify room ID and password are correct
   - Check if room already exists when creating

3. **Nickname Issues**
   - Ensure nickname is unique within the room

4. **Server Not Starting**
   - Check if port is already in use
   - Verify Python and PyQt5 are properly installed

## Project Structure

```
chat-application/
├── server.py          # Server application with admin GUI
├── client.py          # Client application
├── README.md          # This file
└── requirements.txt   # Python dependencies
```

## Development

### Extending Functionality

1. **Adding New Features**:
   - Modify both server and client code
   - Update protocol handling on both ends
   - Test thoroughly

2. **Protocol Changes**:
   - Maintain backward compatibility when possible
   - Update status codes and message formats consistently

3. **UI Improvements**:
   - Modify PyQt5 layouts and widgets
   - Add new signal-slot connections as needed

### Testing

Test the application by:
1. Running multiple client instances
2. Creating multiple rooms
3. Testing edge cases (disconnections, invalid inputs)
4. Verifying admin functions work correctly

## License

This project is open source and available under the MIT License.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
