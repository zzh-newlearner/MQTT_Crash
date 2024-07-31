# Summary
A memory leak has been identified in the nanomq v0.21.9 MQTT broker, which can result in elevated memory consumption and possible instability. This issue could degrade performance and potentially lead to server crashes, affecting overall service availability and reliability.

# Version
nanomq v0.21.9

# Leak Information
```
==27404== 640 bytes in 10 blocks are definitely lost in loss record 279 of 358
==27404==    at 0x4C376D3: calloc (vg_replace_malloc.c:1595)
==27404==    by 0x478295: nni_zalloc (posix_alloc.c:26)
==27404==    by 0x4B4A95: property_alloc (mqtt_codec.c:3491)
==27404==    by 0x4B58E5: property_dup (mqtt_codec.c:3777)
==27404==    by 0x4B698A: property_pub_by_will (mqtt_codec.c:4094)
==27404==    by 0x44EFDF: server_cb (broker.c:720)
==27404==    by 0x473F73: nni_taskq_thread (taskq.c:50)
==27404==    by 0x4752CA: nni_thr_wrap (thread.c:94)
==27404==    by 0x47AC66: nni_plat_thr_main (posix_thread.c:266)
==27404==    by 0x4E4ABDF: start_thread (pthread_create.c:486)
==27404==    by 0x55753BE: clone (clone.S:95)
==27404== 
```