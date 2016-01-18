# ESP8266RelayManager

<img src="https://cloud.githubusercontent.com/assets/2000473/12383915/b0fe419c-bdb4-11e5-8514-7357cd682b5a.png" width="300" align="right"/>

A simple 2 channel relay manager for the ESP8266 with a web inteface and API.

I use this with an ESP8266-01 and a relay board similar to http://modtronix.com/mod-rly2-5v.html. This uses https://github.com/tzapu/WiFiManager which you'll need to install by following their instructions.

## How to configure
Because this uses the wonderful WifiManager project, when you first power the ESP up it will not know how to connect to your network, and instead it will create a Wifi AP that you can connect and then give it the details for your network. If at any point in the future it fails to connect to your wifi (eg. you change your password) it will go back into AP mode so that you can configure it again.

I've set mine up to connect to the wifi and then start hosting the web server on 192.168.0.20. Make that IP something outside of your DHCP range.

If you're not using the ESP8266-01 you will probably need to change the pin configurations.

## Using the Web Interface
Open your browser to http://192.168.0.20/ and you should get a pretty self explanatory interface with two buttons.

## Using the API
The API is RESTful so expects you to use GET and POST. It returns JSON.

### HTTP GET to read the relay state

`GET http://192.168.0.20/api/relay1` returns an HTTP 200 and :
```
{
  "state": 1
}
```

1 = Relay is on. 0 = Relay is off.

### HTTP POST to set the relay state.

POST http://192.168.0.20/api/relay2 with a POST form variable called `state` and it's value set to `0` or `1` (on or off).

You'll receive a response like:
```
{
  "state": 1,
  "set": 1
}
```

Where state=1 means the relay is on, and set=1 means you've just set it that way.


## Notes
* If you'd like to simply toggle a relay you can call http://192.168.0.20/relay2/toggle etc. 
* Many thanks to https://github.com/tzapu/WiFiManager for making WifiManager 
