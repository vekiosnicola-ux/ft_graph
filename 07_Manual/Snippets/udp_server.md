---
tags: [CheatSheet, Snippet]
date: 2026-03-29
status: complete
---


# udp_server.c

```c
 <stdio.h>      // Default System Calls
 <stdlib.h>     // Needed for OS X
 <string.h>     // Needed for Strlen
 <sys/socket.h> // Needed for socket creating and binding
 <netinet/in.h> // Needed to use struct sockaddr_in
 <time.h>       // To control the timeout mechanism

int main( void )
{
    int fd;
    if ( (fd = socket(AF_INET, SOCK_DGRAM, 0)) < 0 ) {
        perror( "socket failed" );
        return 1;
    }

    struct sockaddr_in serveraddr;
    memset( &serveraddr, 0, sizeof(serveraddr) );
    serveraddr.sin_family = AF_INET;
    serveraddr.sin_port = htons( 50037 );
    serveraddr.sin_addr.s_addr = htonl( INADDR_ANY );

    if ( bind(fd, (struct sockaddr *)&serveraddr, sizeof(serveraddr)) < 0 ) {
        perror( "bind failed" );
        return 1;
    }

    char buffer[200];
    for ( int i = 0; i < 100; i++ ) {
        int length = recvfrom( fd, buffer, sizeof(buffer) - 1, 0, NULL, 0 );
        if ( length < 0 ) {
            perror( "recvfrom failed" );
            break;
        }
        buffer[length] = '\0';
        int n = (int)time(NULL);
        int timestamp = buffer[0] << 24 | buffer[1] << 16 | buffer[2] << 8 | buffer[3];

        printf( "%dsd ago - %d bytes (4 bytes for timestamp): '%s'\n", n - timestamp, length, buffer+4 );
    }

    close( fd );
}
```
