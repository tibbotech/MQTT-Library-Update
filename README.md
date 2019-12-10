# MQTT Library Update

This update allows for publishing and receiving of MQTT packets of up to 16383 bytes. 



To publish:

1. Set the flag to allow publishing of larger packets by adding the following line in **global.tbh**:

   `#define MQTT_LARGE_PACKETS 1`

2. Call *mqtt_start_publish()*

   - <b>topic</b> - Name of the topic to be published
   - <b>qos</b> - QoS level
   - <b>length</b> - Total length of the payload to be sent

3. Call *mqtt_continue_publish()*

   - <b>data</b> - Data to be sent. Cannot exceed 255 bytes. 
     This subroutine should be called until the number of  bytes set in *mqtt_start_publish* has been reached. Exceeding this number will result in an error. To send the next packet, *mqtt_start_publish* should be called again.



To receive:

1. Set the flag to allow publishing of larger packets by adding the following line in **global.tbh**:

   `#define MQTT_LARGE_PACKETS 1`

2. *callback_mqtt_notif()* now returns 3 values:

   - <b>topic</b> - Name of the topic received
   - <b>data</b> - Data received
   - <b>length</b> - Total number of bytes remaining to be received. When this value is 0, the entire packet has been received.
     	