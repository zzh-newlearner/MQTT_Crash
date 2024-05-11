# Summary
An exploitable null pointer dereference vulnerability exists in the latest main branch code of Mongoose when handling MQTT packets. A specially crafted MQTT packet can lead to a null pointer dereference, causing the program to crash. This vulnerability could potentially be exploited for a denial-of-service attack.

# Version
Cesanta Mongoose latest main branch code as of commit `b316989` (2024-05-10).

# Crash Information
This vulnerability can be triggered by sending bytes from the [poc](./POC/mongoose_null_pointer.sh) to the tutorial mqtt-server example. The crash occurs in the scpy function at line 125 of the src/fmt.c file, when the function attempts to read from a memory location with an address of 0.
```
AddressSanitizer:DEADLYSIGNAL
=================================================================
==6184==ERROR: AddressSanitizer: SEGV on unknown address 0x000000000000 (pc 0x00000040873e bp 0x7ffd9bada200 sp 0x7ffd9bada1d0 T0)
==6184==The signal is caused by a READ memory access.
==6184==Hint: address points to the zero page.
    #0 0x40873d in scpy src/fmt.c:125
    #1 0x409e4f in mg_vxprintf src/fmt.c:207
    #2 0x41b8c4 in mg_log src/log.c:43
    #3 0x4029dd in fn mongoose/tutorials/mqtt/mqtt-server/main.c:87
    #4 0x407027 in mg_call src/event.c:22
    #5 0x4230bb in mqtt_cb src/mqtt.c:496
    #6 0x406fd5 in mg_call src/event.c:21
    #7 0x431a92 in iolog src/sock.c:108
    #8 0x433814 in read_conn src/sock.c:297
    #9 0x43812e in mg_mgr_poll src/sock.c:711
    #10 0x4036a9 in main mongoose/tutorials/mqtt/mqtt-server/main.c:144
    #11 0x7fbe70bf544a in __libc_start_main ../csu/libc-start.c:308
    #12 0x401d79 in _start (mongoose/tutorials/mqtt/mqtt-server/example+0x401d79)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV src/fmt.c:125 in scpy
==6184==ABORTING
```