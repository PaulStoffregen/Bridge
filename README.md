Bridge Library For Any Boards
=============================

This is a slightly modified copy of the Bridge library used on Arduino Yún.

`Bridge.begin()` is extended to allow any serial or even non-serial port (USB Serial, Ethernet, etc) to be used.  Of course, a Linux system with the Bridge protocol must be present on the other side of the communication channel.

To use the alternate begin for hardware serial, simply give the port name.

        Bridge.begin(Serial3);

Optionally, the baud rate can be specified.

        Bridge.begin(Serial2, 921600);  // faster baud rate,  default is 250000

To use a port than is not hardware serial, first set up its communication, then give the name to Serial.begin().

        SoftwareSerial mySoftSer(8,9);

        void setup() {
          mySoftSer.begin(38400);
          Bridge.begin(mySoftSer);
        }

In theory, any communication channel based on Arduino Stream may be used.  In practice, USB Serial and hardware serial are likely the only ones with good enough performance.  But perhaps Ethernet could work?

        EthernetClient client;

        void setup() {
          if (Ethernet.begin(mac)) {
            if (client.connect(server, 4321)) {
              Bridge.begin(client);
            }
          }
        }


