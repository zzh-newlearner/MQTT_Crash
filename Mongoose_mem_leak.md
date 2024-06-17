# Summary
A direct memory leak of 21,400 bytes in 535 objects has been detected in the Mongoose MQTT server code. The leak is attributed to a series of function calls, starting from a calloc allocation and propagating through various functions in the codebase. This issue could lead to increased memory usage and potential stability problems in the server.

# Version
Cesanta Mongoose latest main branch code as of commit `b316989` (2024-05-10).

# Leak Information
Direct leak of 21400 byte(s) in 535 object(s) allocated from:
    #0 0x7f47c6c4d82e in calloc (/lib64/libasan.so.5+0x10c82e)
    #1 0x402c67 in fn mongoose/tutorials/mqtt/mqtt-server/main.c:81
    #2 0x4087fb in mg_call src/event.c:22
    #3 0x42c4c9 in mqtt_cb src/mqtt.c:496
    #4 0x408785 in mg_call src/event.c:21
    #5 0x43d769 in iolog src/sock.c:108
    #6 0x43feb9 in read_conn src/sock.c:297
    #7 0x445842 in mg_mgr_poll src/sock.c:711
    #8 0x403fbd in main mongoose/tutorials/mqtt/mqtt-server/main.c:144
    #9 0x7f47c67aa44a in __libc_start_main ../csu/libc-start.c:308