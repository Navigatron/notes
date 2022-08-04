
```bash
#!/bin/bash

exec 3<>/dev/tcp/www.northwesternmutual.com/443
echo -e "GET / HTTP/1.1\r\nHost: www.northwesternmutual.com\r\nAccept: */*\r\nConnection: close\r\n\r\n" >&3
cat <&3
```
