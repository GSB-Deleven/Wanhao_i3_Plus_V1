# Save settings here

`sudo nano /etc/rc.local`

## Mine looks like this

```shell
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

# Print the IP address
_IP=$(hostname -I) || true
if [ "$_IP" ]; then
  printf "My IP address is %s\n" "$_IP"
fi


/sbin/iptables -t mangle -I POSTROUTING 1 -o wlan0 -p udp --dport 123 -j TOS --set-tos 0x00


echo
echo "------------------------------------------------------------"
echo
echo "You may now open a web browser on your local network and "
echo "navigate to any of the following addresses to access "
echo "OctoPrint:"
echo
for name in $_NAME;
do
    echo " http://$name.local"
done

for ip in $(hostname -I);
do 
    echo "    http://$ip"
done

echo
echo "https is also available, with a self-signed certificate."
echo 
echo "------------------------------------------------------------"
echo
v4l2-ctl --set-ctrl=focus_auto=0
v4l2-ctl --set-ctrl=focus_absolute=40
sudo v4l2-ctl --set-ctrl=zoom_absolute=100
sudo v4l2-ctl --set-ctrl=exposure_absolute=80 
exit 0
```

## The part I added is:

```bash
v4l2-ctl --set-ctrl=focus_auto=0
v4l2-ctl --set-ctrl=focus_absolute=40
sudo v4l2-ctl --set-ctrl=zoom_absolute=100
sudo v4l2-ctl --set-ctrl=exposure_absolute=80 
```

# If you want to see all the options type 

`sudo v4l2-ctl -l`  
  
Mine looks like this:

```
pi@octopi:~ $ sudo v4l2-ctl -l 
                     brightness 0x00980900 (int)    : min=0 max=255 step=1 default=128 value=128
                       contrast 0x00980901 (int)    : min=0 max=255 step=1 default=128 value=128
                     saturation 0x00980902 (int)    : min=0 max=255 step=1 default=128 value=128
 white_balance_temperature_auto 0x0098090c (bool)   : default=1 value=1
                           gain 0x00980913 (int)    : min=0 max=255 step=1 default=0 value=0
           power_line_frequency 0x00980918 (menu)   : min=0 max=2 default=2 value=2
      white_balance_temperature 0x0098091a (int)    : min=2000 max=6500 step=1 default=4000 value=2811 flags=inactive
                      sharpness 0x0098091b (int)    : min=0 max=255 step=1 default=128 value=128
         backlight_compensation 0x0098091c (int)    : min=0 max=1 step=1 default=0 value=0
                  exposure_auto 0x009a0901 (menu)   : min=0 max=3 default=3 value=1
              exposure_absolute 0x009a0902 (int)    : min=3 max=2047 step=1 default=250 value=79
         exposure_auto_priority 0x009a0903 (bool)   : default=0 value=1
                   pan_absolute 0x009a0908 (int)    : min=-36000 max=36000 step=3600 default=0 value=0
                  tilt_absolute 0x009a0909 (int)    : min=-36000 max=36000 step=3600 default=0 value=0
                 focus_absolute 0x009a090a (int)    : min=0 max=250 step=5 default=0 value=40
                     focus_auto 0x009a090c (bool)   : default=1 value=0
                  zoom_absolute 0x009a090d (int)    : min=100 max=500 step=1 default=100 value=100
```
