# Summary
A crash has been identified in the nanomq v0.21.9 MQTT broker due to an invalid read of size 4. This issue can lead to server instability and crashes, which may degrade performance and impact overall service availability and reliability.

# Version
nanomq v0.21.9

# Crash detail
```
==31841== Thread 57 nng:task:
==31841== Invalid read of size 4
==31841==    at 0x4621AF: id_find (idhash.c:101)
==31841==    by 0x462329: nni_id_get (idhash.c:130)
==31841==    by 0x4BAB3B: nni_qos_db_get (mqtt_qos_db_api.c:35)
==31841==    by 0x490288: nano_pipe_recv_cb (nmq_mqtt.c:1160)
==31841==    by 0x4746C6: nni_task_exec (taskq.c:144)
==31841==    by 0x45D544: nni_aio_finish_impl (aio.c:469)
==31841==    by 0x45D618: nni_aio_finish_sync (aio.c:484)
==31841==    by 0x538FE1: tcptran_pipe_recv_cb (broker_tcp.c:892)
==31841==    by 0x473F73: nni_taskq_thread (taskq.c:50)
==31841==    by 0x4752CA: nni_thr_wrap (thread.c:94)
==31841==    by 0x47AC66: nni_plat_thr_main (posix_thread.c:266)
==31841==    by 0x4E4ABDF: start_thread (pthread_create.c:486)
==31841==  Address 0x8 is not stack'd, malloc'd or (recently) free'd
==31841== 
==31841== 
==31841== HEAP SUMMARY:
==31841==     in use at exit: 5,957,269 bytes in 1,985 blocks
==31841==   total heap usage: 4,700 allocs, 2,715 frees, 6,530,383 bytes allocated
```