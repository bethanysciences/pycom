wlan.connect(ssid='iotworld', auth=(WLAN.WPA2, 'iotworld'))
10.0.0.33

machine  
-----------------------------------------------------------------------
import machine
help(machine)                   # display all members from the machine module
machine.freq()                  # get the CPU frequency
machine.unique_id()             # return the 6-byte unique board id
from machine import RTC
rtc = RTC()
rtc.init((2018, 6, 24, 21, 04, 0, 0, 0))
print(rtc.now())

pycom
-----------------------------------------------------------------------
import pycom
pycom.heartbeat(False)          # disable the heartbeat LED
pycom.heartbeat(True)           # enable the heartbeat LED
pycom.heartbeat()               # get the heartbeat state
pycom.rgbled(0xff00)            # make the LED light up in green color
pycom.nvs_set(key, value)       # Non volitile memory
pycom.nvs_set('count', 25)      # Set NVRAM memory area
pycom.nvs_get('count')          # Get value
pycom.nvs_erase(key)
pycom.nvs_erase_all()
pycom.wifi_on_boot([enable])
pycom.wifi_on_boot(True)        # enable WiFi on boot
pycom.wifi_on_boot()            # get the wifi on boot flag

network
-----------------------------------------------------------------------
import network
import time
wlan.connect(ssid, * , auth=None, bssid=None, timeout=None, ca_certs=None, keyfile=None, certfile=None, identity=None)
  mode: WLAN.STA, WLAN.AP or WLAN.STA_AP
  ssid: assigned ssid
  auth: WLAN.WEP, WLAN.WPA or WLAN.WPA2
  antenna: WLAN.INT_ANT, WLAN.EXT_ANT
  power_save: for STA mode
  hidden: beacon ssid  
wlan.scan()                                                 # scan for networks
wlan.disconnect()
wlan.isconnected()
wlan.antenna([antenna])                                     # antenna type
wlan.deinit()                                               # disable WiFi radio.
while not wlan.isconnected():
    time.sleep_ms(50)
print(wlan.ifconfig())
wlan = WLAN(mode=WLAN.STA)
server = network.Server()
server.deinit()                                             # disable server
server.init(login=('user', 'password'), timeout=600)        # enable the server
server = Server(login=('user', 'password'), timeout=60)     # re-init
server.timeout(300)                                         # change timeout
server.timeout()                                            # get timeout
server.isrunning()                                          # check

AWS
-----------------------------------------------------------------------
https://docs.pycom.io/chapter/tutorials/all/aws.html

MQTT
-----------------------------------------------------------------------
io.adafruit.com  
user bethanysciences
key 8fe969b577893c94dcdc52b0f6f3625677427091
from mqtt import MQTTClient
from network import WLAN
import machine
import time
def sub_cb(topic, msg):
   print(msg)
wlan = WLAN(mode=WLAN.STA)
wlan.connect("yourwifinetwork", auth=(WLAN.WPA2, "wifipassword"), timeout=5000)
while not wlan.isconnected():  
    machine.idle()
print("Connected to Wifi\n")
client = MQTTClient("device_id", "io.adafruit.com",user="your_username", password="your_api_key", port=1883)
client.set_callback(sub_cb)
client.connect()
client.subscribe(topic="youraccount/feeds/lights")
while True:
    print("Sending ON")
    client.publish(topic="youraccount/feeds/lights", msg="ON")
    time.sleep(1)
    print("Sending OFF")
    client.publish(topic="youraccount/feeds/lights", msg="OFF")
    client.check_msg()
    time.sleep(1)
from mqtt import MQTTClient
from network import WLAN
import machine
import time
def sub_cb(topic, msg):
   print(msg)
wlan = WLAN(mode=WLAN.STA)
wlan.connect("yourwifinetwork", auth=(WLAN.WPA2, "wifipassword"), timeout=5000)
while not wlan.isconnected():  
    machine.idle()
print("Connected to Wifi\n")
client = MQTTClient("device_id", "io.adafruit.com",user="your_username", password="your_api_key", port=1883)
client.set_callback(sub_cb)
client.connect()
client.subscribe(topic="youraccount/feeds/lights")
while True:
    print("Sending ON")
    client.publish(topic="youraccount/feeds/lights", msg="ON")
    time.sleep(1)
    print("Sending OFF")
    client.publish(topic="youraccount/feeds/lights", msg="OFF")
    client.check_msg()
    time.sleep(1)

    serial address /dev/cu.usbmodemPy343431
    AP connection 192.168.4.1
{
    "address": "10.0.0.33",
    "username": "micro",
    "password": "python",
    "sync_folder": "",
    "open_on_start": true,
    "statusbar_buttons": [
        "console",
        "run",
        "upload",
        "download"
    ],
    "sync_file_types": "py,txt,log,json,xml",
    "ctrl_c_on_connect": false
}