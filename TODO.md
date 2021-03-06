#TODO
 
## Core / DNS
- [ ] Redo AXFR logs
- [ ] Access to the hotcache and the cfg_table via FUNs
- [ ] (1) Terminate updating zones during config reload
- [ ] (1) Clean up the code & add comments
- [ ] (*) saveZones - doesn't correctly save zones if there a lot of updates. Save strategy based on update size and time and currently running updates.
- [ ] Logs level startup config
- [ ] Check delete in ioc2rpz: rpz_hotcache_table/pkthotcache

- [ ] Mnesia for storage (and auto creation)
- [ ] Distributed configuration
- [ ] Wait while a remote server confirms receiving a notification
- [ ] (2) EDNS0 Support: DNS Cookie, edns-tcp-keepalive, NSID
- [ ] (3) Memory optimization for huge zones (erl -pa ebin +MEas bf ?????)
- [ ] DoH https://tools.ietf.org/html/rfc8484
- [ ] DoD https://tools.ietf.org/html/draft-ietf-dprive-dnsodtls-06

- [ ] EUnit Tests

## Sources
- [ ] Add script for RPZ via "shell:"
- [ ] Add source PostreSQL, MySQL via "shell:"
- [ ] RPZ action per source
- [ ] (2) Source based on files check by mod.date and size -> read by chunks
- [ ] Retry if source is not available
- [ ] Simultanious source downloads

- [ ] ioc type in config
- [x] max # of IOCs
- [ ] max file size
- [ ] RPZ action
- [ ] NS type
- [ ] lowcase optimization option
  - [ ] (1) IOC to lowercase - check memory usage impact (in ioc2rpz_conn)
- [ ] spawn processes
- [ ] Hot cache optimization depending on RPZ refresh time and source usage in multiple feeds
- [ ] Cache optimization for huge zones
- [ ] Statistics table


## RPZ
- [ ] RPZ by source intersection
- [ ] Max # of IOCs
- [ ] Catalog zones
- [ ] Statistics per zone (# records, last update, # AXFR, # IXFR, last axfr update time, avg axfr update time, last ixfr update time, avg ixfr update time)
- [ ] RPZ behavior: ignore unreachable sources, use old data for unreachable sources, do not update the zone
- [ ] Additional local records: ptr, srv, mx etc
- [ ] An action per source: {"",action,locdata} //default action ,{"source_name",action,locdata}
- [ ] RPZ transfer rate limiting

- [ ] (2) FDateTime,ToDateTime,FDateTimeZ,ToDateTimeZ + support them for AXFR  
[:FDateTime:] = "2017-10-13 13:13:13", [:FDateTimeZ:] = "2017-10-13T13:13:13Z"  
[:ToDateTime:] = "2017-10-13 13:13:13", [:ToDateTimeZ:] = "2017-10-13T13:13:13Z"


## Servers
- [ ] Enforcement max # of IOCs
- [ ] Secondary DNS via MNESIA and distributed

## REST
- [ ] MGMT via REST API
  - [ ] Statistics per source, RPZ, performance
  - [ ] Bug RPZ stats after reload config
- [ ] Bug in cowboy. Can not send 501 in "catch all"

## Configuration
- [.] Validate: Configuration file name pass as a variable to the container

## Management
- [ ] DNS health check requests
- [ ] Disable MGMT via DNS (update ioc2rpz.gui first) - default behaviour


## Unsorted
- [ ] Performance testing vs bind:
  - [ ] 1 core/8GB RAM: start time, zone transfer time, zone size, CPU, Memory
    - [ ] 100k rules
    - [ ] 1M rules
    - [ ] 10M rules
  - [ ] 4 cores/32 GB RAM: start time, zone transfer time, zone size
    - [ ] 100k rules
    - [ ] 1M rules
    - [ ] 10M rules
- [ ] Switch from IXFR cache to Sources cache. IXFR cache allows you to support less zone updates but IOCs can be stored multiple times. Sources cache will contain duplicate IOCs from the same source but RPZs will be updated more frequently (looks like it is not bad).
  - [ ] (3) Share IOC between the feeds in IXFR table (do not forget about different whitelists)

## Other/optimization TODO
- [ ] (1) Do not cache expired IOCs if ExpDateTime<Serial_IXFR / update ExpDateTime if exists
- [ ] (1) Check zones IXFR update from multiple sources
- [x] (2) UDP & TableMGMT under supervisors
