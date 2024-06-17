# Summary
A memory leak has been detected in the Mosquitto MQTT server, which can lead to increased memory usage and potential server instability. This degradation in performance may eventually cause the server to crash, impacting service availability and reliability.

# Version
mosquitto v2.0.14

# Leak Information
```
==1660== HEAP SUMMARY:
==1660==     in use at exit: 624 bytes in 17 blocks
==1660==   total heap usage: 3,391,161 allocs, 3,391,144 frees, 15,356,711,225 bytes allocated
==1660== 
==1660== 560 (440 direct, 120 indirect) bytes in 5 blocks are definitely lost in loss record 5 of 5
==1660==    at 0x4C376D3: calloc (vg_replace_malloc.c:1595)
==1660==    by 0x4218F8: mosquitto__calloc (memory_mosq.c:58)
==1660==    by 0x41BF6F: will__read (handle_connect.c:338)
==1660==    by 0x41BF6F: handle__connect (handle_connect.c:652)
==1660==    by 0x432E8C: handle__packet (read_handle.c:64)
==1660==    by 0x4287A9: packet__read (packet_mosq.c:553)
==1660==    by 0x4228A4: loop_handle_reads_writes (mux_epoll.c:295)
==1660==    by 0x4228A4: mux_epoll__handle (mux_epoll.c:207)
==1660==    by 0x4220D0: mux__handle (mux.c:76)
==1660==    by 0x421227: mosquitto_main_loop (loop.c:205)
==1660==    by 0x406672: main (mosquitto.c:562)
==1660== 
==1660== LEAK SUMMARY:
==1660==    definitely lost: 440 bytes in 5 blocks
==1660==    indirectly lost: 120 bytes in 10 blocks
==1660==      possibly lost: 0 bytes in 0 blocks
==1660==    still reachable: 64 bytes in 2 blocks
==1660==         suppressed: 0 bytes in 0 blocks
==1660== Reachable blocks (those to which a pointer was found) are not shown.
==1660== To see them, rerun with: --leak-check=full --show-leak-kinds=all
==1660== 
==1660== For lists of detected and suppressed errors, rerun with: -s
==1660== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
```