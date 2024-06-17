# Summary
A memory leak has been detected in the Mosquitto MQTT server code, which could lead to increased memory usage and potential stability issues over time. This can degrade performance and may eventually cause the server to crash, impacting the availability and reliability of the service.

# Version
mosquitto v2.0.14

# Leak Information
```
==33200== HEAP SUMMARY:
==33200==     in use at exit: 103,075 bytes in 3,420 blocks
==33200==   total heap usage: 4,164 allocs, 744 frees, 149,901 bytes allocated
==33200== 
==33200== 6 bytes in 1 blocks are definitely lost in loss record 1 of 679
==33200==    at 0x4C3007D: malloc (vg_replace_malloc.c:442)
==33200==    by 0x5D27359: strdup (strdup.c:42)
==33200==    by 0x41733D: mosquitto__strdup (memory_mosq.c:152)
==33200==    by 0x40DE4A: config__check (conf.c:2296)
==33200==    by 0x40DE4A: config__parse_args (conf.c:527)
==33200==    by 0x40580E: main (mosquitto.c:494)
==33200== 
==33200== 8 bytes in 1 blocks are definitely lost in loss record 4 of 679
==33200==    at 0x4C376D3: calloc (vg_replace_malloc.c:1595)
==33200==    by 0x417190: mosquitto__calloc (memory_mosq.c:58)
==33200==    by 0x42791E: mosquitto_security_init_default (security_default.c:65)
==33200==    by 0x4058C6: main (mosquitto.c:532)
==33200== 
==33200== 10 bytes in 1 blocks are definitely lost in loss record 5 of 679
==33200==    at 0x4C3007D: malloc (vg_replace_malloc.c:442)
==33200==    by 0x5D27359: strdup (strdup.c:42)
==33200==    by 0x41733D: mosquitto__strdup (memory_mosq.c:152)
==33200==    by 0x40DD9C: config__parse_args (conf.c:519)
==33200==    by 0x40580E: main (mosquitto.c:494)
==33200== 
==33200== 736 bytes in 1 blocks are definitely lost in loss record 647 of 679
==33200==    at 0x4C378DF: realloc (vg_replace_malloc.c:1690)
==33200==    by 0x4172C2: mosquitto__realloc (memory_mosq.c:130)
==33200==    by 0x40618D: listeners__start_local_only (mosquitto.c:306)
==33200==    by 0x406354: listeners__start (mosquitto.c:345)
==33200==    by 0x406354: listeners__start (mosquitto.c:338)
==33200==    by 0x405958: main (mosquitto.c:551)
==33200== 
==33200== LEAK SUMMARY:
==33200==    definitely lost: 760 bytes in 4 blocks
==33200==    indirectly lost: 0 bytes in 0 blocks
==33200==      possibly lost: 0 bytes in 0 blocks
==33200==    still reachable: 102,315 bytes in 3,416 blocks
==33200==         suppressed: 0 bytes in 0 blocks
==33200== Reachable blocks (those to which a pointer was found) are not shown.
==33200== To see them, rerun with: --leak-check=full --show-leak-kinds=all
==33200== 
==33200== For lists of detected and suppressed errors, rerun with: -s
==33200== ERROR SUMMARY: 4 errors from 4 contexts (suppressed: 0 from 0)
```