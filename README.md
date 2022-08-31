# env
my dev environment

## desc

| name          | node port | physical port  | desc                            |
| ------------- | --------- | -------------- | ------------------------------- |
| zookeeper     | 2181      | 2181,2182,2183 |                                 |
| kafka         | 9092      | 9092           |                                 |
| node-exporter | 9100      | 9100           |                                 |
| altermanager  | 9093      | 9093           |                                 |
| cadvisor      | 8087      | 8087           |                                 |
| grafana       | 3000      | 3000           | user admin<br />password 123456 |
| mysql         | 3306      | 3306           | root/123456                     |
| redis         | 6379      | 16379          | password 123456                 |

## error

### Error opening query log file

> it's very often when we init prometheus, we may encountered this error:
>
> [err="open /prometheus/queries.active: permission denied"](https://github.com/prometheus/prometheus/issues/5976)
>
> ```
> error:
> level=info ts=2019-08-30T05:14:43.159Z caller=main.go:293 msg="no time or size retention was set so using the default time retention" duration=15d
> level=info ts=2019-08-30T05:14:43.159Z caller=main.go:329 msg="Starting Prometheus" version="(version=2.12.0, branch=HEAD, revision=43acd0e2e93f9f70c49b2267efa0124f1e759e86)"
> level=info ts=2019-08-30T05:14:43.159Z caller=main.go:330 build_context="(go=go1.12.8, user=root@7a9dbdbe0cc7, date=20190818-13:53:16)"
> level=info ts=2019-08-30T05:14:43.159Z caller=main.go:331 host_details="(Linux 3.10.0-957.el7.x86_64 #1 SMP Thu Oct 4 20:48:51 UTC 2018 x86_64 4d7bb264eb92 (none))"
> level=info ts=2019-08-30T05:14:43.160Z caller=main.go:332 fd_limits="(soft=1048576, hard=1048576)"
> level=info ts=2019-08-30T05:14:43.160Z caller=main.go:333 vm_limits="(soft=unlimited, hard=unlimited)"
> level=error ts=2019-08-30T05:14:43.160Z caller=query_logger.go:82 component=activeQueryTracker msg="Error opening query log file" file=/prometheus/queries.active err="open /prometheus/queries.active: permission denied"
> panic: Unable to create mmap-ed active query log
> 
> goroutine 1 [running]:
> github.com/prometheus/prometheus/promql.NewActiveQueryTracker(0x7ffef5ed3f02, 0xb, 0x14, 0x2a6b7c0, 0xc000596cf0, 0x2a6b7c0)
> /app/promql/query_logger.go:112 +0x4d2
> main.main()
> /app/cmd/prometheus/main.go:361 +0x52bd
> ```
>
> **this caused by prometheus's permission, first we enter `echo ${UID}` in our machine, then add `user: "${UID}:${UID}"` will fix it.**
