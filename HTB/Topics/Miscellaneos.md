
### 1. Reverse Shell vs Bind Shell
A reverse shell is done by setting up a listener on a port at the host machine and on the target we specify the IP of the host machine and the port which is listening and we sent the **/bin/bash** on that port.
A bind shell is achieved by setting up a listener on the target which is then going to be open on a port. The host will connect to the target on that host and when the connection request is made then the target will execute the **/bin/bash** .

