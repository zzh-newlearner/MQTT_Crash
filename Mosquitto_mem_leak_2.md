# Summary
A memory leak has been identified in the Mosquitto MQTT server, which poses a risk of increased memory usage and potential server instability. This can lead to performance degradation and possibly cause the server to crash, affecting service availability and reliability.

# Version
mosquitto v2.0.14

# Leak Information
```
==8338== HEAP SUMMARY:
==8338==     in use at exit: 210 bytes in 7 blocks
==8338==   total heap usage: 183,034 allocs, 183,027 frees, 54,369,378,307 bytes allocated
==8338==
==8338== 146 (48 direct, 98 indirect) bytes in 1 blocks are definitely lost in loss record 7 of 7
==8338==    at 0x4C376D3: calloc (vg_replace_malloc.c:1595)
==8338==    by 0x4218F8: mosquitto__calloc (memory_mosq.c:58)
==8338==    by 0x42B1A6: property__read_all (property_mosq.c:166)
==8338==    by 0x41D454: handle__pubackcomp (handle_pubackcomp.c:88)
==8338==    by 0x432E69: handle__packet (read_handle.c:52)
==8338==    by 0x4287A9: packet__read (packet_mosq.c:553)
==8338==    by 0x4228A4: loop_handle_reads_writes (mux_epoll.c:295)
==8338==    by 0x4228A4: mux_epoll__handle (mux_epoll.c:207)
==8338==    by 0x4220D0: mux__handle (mux.c:76)
==8338==    by 0x421227: mosquitto_main_loop (loop.c:205)
==8338==    by 0x406672: main (mosquitto.c:562)
==8338== 
==8338== LEAK SUMMARY:
==8338==    definitely lost: 48 bytes in 1 blocks
==8338==    indirectly lost: 98 bytes in 4 blocks
==8338==      possibly lost: 0 bytes in 0 blocks
==8338==    still reachable: 64 bytes in 2 blocks
==8338==         suppressed: 0 bytes in 0 blocks
==8338== Reachable blocks (those to which a pointer was found) are not shown.
==8338== To see them, rerun with: --leak-check=full --show-leak-kinds=all
==8338== 
==8338== For lists of detected and suppressed errors, rerun with: -s
==8338== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
```