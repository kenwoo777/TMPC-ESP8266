the codebase, 9000-line, becomes a beast of ESP8266.

1. as the name implies, it is used as a codebase for ESP8266; currently is Gen1; future would add the MultiTimers/PWMs and in-depth GPIO/INT timings as Gen2.
2. this codebase provides some fundamental facilities which might be sufficient for common uses; might be more powerful then before/just take a trial. use http-uri "/listcmds" at runtime would reveal, as to run each uri that provided.
3. well-applying the mDns is one of the main features, you could experienced by playing the EX1.
4. another important feature, the "accurately time synchronization", which after the sync, among devices(2 to 19 devices theoretically applicable), "at the same time", the time deviations are <30us; <5ms during an hour
   and probably <100ms after 3 days. that is of the time-compensation taken effectively. if no such a compensation, deviation is as high as 5 seconds/3days.
5. of this codebase, thoroughly temporal controls cast the ESP8266 into another applicable layer. hope it benefits.

## For evaluating EX1,

### a. add the ssid/password entry that your wifi-ap provides to

const char *const WIFI_CRED_STA[][2]={ // wifi credential, for sta role.

-->    {"myssid", "mypw"},

    {"ESP_TESTAP", "87654321"},
    
    {"Office", "123456"},
    
    {"Xperia X Performance_bc10", "e848acbcfd98"},
    
    {"etc", "etc"},
    
};

### b. since this codebase uses my another lib "Esp8266Vars2File.h" which is expanded/resides in the codebase "tmpc_esp8266.pde":
between the marks,

// ****************************************************** you can remove this block of code and use as lib by #include"Esp8266Vars2File.h"

#### please copy and paste into a created file Esp8266Vars2File.h and put it into ex1 folder.

### c. in Arduino IDE, choose at this option, "Flash Size", with nonzero FS size which is needed.

### d. prepare 6 devices, e.g., WeMos D1 mini;
        however 2 to 19 are applicable.
        if number of devices other than 6, the ex1-code would need to modify:

        #define CLIDEVS 5 // set 5 means 1 host and 5 clients.

        for example, you only have 2 wemos-d1-mini to be used, then set CLIDEVS 1

### above all that is it; flash the same code to every devices, yes, the same. and power them on, EX1 would demonstrate.

after they running for 15 minutes(while all are at a minimal deviation state), you can probe the time deviation among them on GPIO2.

note the auto-gened addresses are http://esp8266-iot-espnow_ts-@.local/ where the @ is no-dash, 2, 3, 4, ..., to CLIDEVS.

try to, e.g., http://esp8266-iot-espnow_ts-2.local/listcmds

UART is on at 115200,8,n,1,n

note: the number of running devices less than the set (CLIDEVS+1) would keep them in STA state; otherwise all would enter espnow mode few minutes later for syncing. (so use less than set to evaluate http stuffs).

## more details please refer to the comments in each example code.
