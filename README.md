# Fan control for TerraMaster on Linux 

Tested with F4-220. This a direct port of the Xpenology fancontrol script by Eudean to work on OMV/Debian.

Original author: https://xpenology.com/forum/topic/14007-terramaster-f4-220-fan-control/?ct=1559481439

## Installation:
1. Clone the repo
``git clone https://github.com/ahmedmagdiosman/terramaster-fancontrol.git``

2. Build with GCC. I'm using the docker image for ease of use.

   - Pull the image:

``docker pull gcc``

   - Compile fancontrol.cpp (you must be in the same directory)

``docker run --rm -v "$PWD":/usr/src/myapp -w /usr/src/myapp gcc gcc -o fancontrol fancontrol.cpp``


3. Create a directory containing all the drives. I created a directory in ``/opt/disks/``  and just empty files inside (as root):
```
mkdir /opt/disks
cd /run/disks
touch sda sdb sdc
```

This far from perfect and if you're a Linux wizard you probably can do something better with regex, e.g.  ``/dev/sd*[a-z]``

4. Run the compiled program (command descriptions in the author's thread).

``sudo ./fancontrol 1 40 ``

This will run it in debug mode (1) with temperature setpoint= 40c. Make sure run with fancontrol with sudo.

5. Alternatively you can use the included systemd service. Copy it to `/etc/systemd/system`. Also, copy the binary to `/usr/local/bin/fancontrol`.

```
sudo systemctl start fancontrol.service
sudo systemctl enable fancontrol.service
```
