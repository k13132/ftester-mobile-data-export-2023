# F-Tester&reg; Open Data 
[![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

This repository contains two anonymized, freely usable datasets of transmission data acquired in the mobile network of three operators in the Czech Republic. The measurements were obtained in a car while driving in the city and the countryside. The data structure is described in the following chapter. The data is licensed under the CC BY-NC-SA 4.0 licence.


## Basic characteristics of the data set
Measurement device: F-Tester&reg; 4drive-box v2 (https://f-tester.fel.cvut.cz)

### Prague
- Date of data acquisition: 2023-09-06
- Time of data acquisition: 09:48:32 CET
- Length of record: 1800 s
- Data file format: JSON

### Jeseníky
- Date of data acquisition: 2023-09-06
- Time of data acquisition: 14:14:05 CET
- Length of record: 1800 s
- Data file format: JSON

## Data files
### Directory structure

```SH
.
└── data
    ├── mobile_measurement-data_Jeseniky.zip
    │   ├── Operator1_Czechia_Jeseniky.json
    │   ├── Operator2_Czechia_Jeseniky.json
    │   └── Operator3_Czechia_Jeseniky.json
    └── mobile_measurement-data_Prague.zip
        ├── Operator1_Czechia_Prague.json
        ├── Operator2_Czechia_Prague.json
        └── Operator3_Czechia_Prague.json
```

#### md5sum
```TXT
a156a15a626cc0441d87be8ebe76c9c6  mobile_measurement-data_Jeseniky.zip
c1b3753bbe205dbeabcd278fe41ccd75  mobile_measurement-data_Prague.zip
319b97c6d3365043f9d38d0e839d7635  01_Prague/Operator1_Czechia_Prague.json
b19f243bd3e71670ba83327855437ff1  01_Prague/Operator2_Czechia_Prague.json
4e89966ab6a02a6e115ad93e6cce41cc  01_Prague/Operator3_Czechia_Prague.json
869cabca0a5bb446c4edb5ed2eb6d58e  02_Jeseniky/Operator1_Czechia_Jeseniky.json
dc1824d3469668918b191f89bf8ae93d  02_Jeseniky/Operator2_Czechia_Jeseniky.json
8dbad2b86d7ac722c37392e272b9208b  02_Jeseniky/Operator3_Czechia_Jeseniky.json
```

## Description of anonymization

All variables that could identify a real mobile operator are anonymized in the data file. The names of the operators are selected: Operator1, Operator2, and Operator3.

List of anonymized items:
- mnc
- cell_id
- ltrac
- tac
- channel
- earfcn
- rx_channel
- netname
- imsi
- nr_channel
- nr_ul_channel
- ipv4-address

## Description of JSON export file

    version 1.0.1 (this document)

    NOTEs:
    - Duplicity in Mobile network info is by design. Statistics are collected via several methods (AT commands, QMI infrastructure).
    - Not all data structures are presents
        - depend on available statistics 
        - depend on available network mode/types
    - Multiple timestamp source / formats available
        - human readable
        - unix timestamp
        - telemetry timestamps (lower sample rate)

### General structure
``` JSON
{
    "info": {},                                     Info section
    "data": {}                                      Data section
}
   ```

#### Info section (Detail)
``` JSON
{
"info": {
    "version": "1.0.0"                              JSON version specification
    "layer": 4                                      RM ISO/OSI Layer specification
},
   ```


#### Data section (Detail)



``` JSON
    "data": {
        "1_U_1": {                                      data record key - TestID_Direction_TimeStamp
            "key": "1_U_1"                              data record key - TestID_Direction_TimeStamp
            "timestamp": 2,                             relative time stamp
            "unix_timestamp": 1676358085,               unix time stamp
            "direction": "upstream",                    traffic flow direction
            "test_id": 3,                               test id
            "ts": 1676358083,                           telemetry timestamp (if telemetry [mobile, system, gps] present)
   ```
<blockquote>

<details><summary>GPS data (When GPS stats are collected)</summary>

``` JSON
        "gps_age": 1,                                  time since last location update
        "gps_HDOP": 0.7,                               horizontal accuracy
        "gps_VDOP": 1.2,                               vertical accuracy
        "gps_PDOP": 1.4,                               3D accuracy
        "gps_satellites": 9,                           number of satelites
        "gps_course": 121.9,                           course [deg]   
        "gps_elevation": 263.2,                        elevation
        "gps_latitude": 50.015739,                     latitude
        "gps_longitude": 14.525863,                    longitude
        "gps_speed": 123.2,                            speed [km/h]
```

</details>

<details><summary>System data (When system stats are collected)</summary>

``` JSON
        "load_1m": 1.21,                               system load (1 minute average)     
        "load_5m": 1.52,                               system load (5 minutes average)
        "load_15m": 1.64,                              system load (15 minutes average)
        "mem_total": 4115771392,                       total memory system memory
        "mem_free": 3975598080,                        free memory available
        "mem_swap_total": 0,                           available swap space
        "mem_swap_free": 0,                            free swap space
```

</details>

<details><summary>Mobile network information (When Mobile network stats are collected)</summary>

<blockquote>
  <details><summary>Modem and Network information </summary>

``` JSON
        "dev_manufacturer": "Telit",                 manufacturer
        "dev_model": "FN980",                        device model
        "dev_revision": "M0H.020202",                FW revision
        "dev_imei": "359661102005457",               IMEI - International Mobile Equipment Identity 
        "dev_temp_pa_therm1": -999,                  modem temperature (1) (optional)
        "dev_temp_tsens4": -999,                     modem temperature (4) (optional)
        "dev_temp_tsens5": -999,                     modem temperature (5) (optional)
        "status": "connected",                       network status
        "l3_state": {                                network layer state L3  
            "uptime": 1737,                          time since mobile network connection was established  
            "device": "wwan0",                       system device name
            "ipv4address": [                         IPv4 addresses - multiple addresses possible
            {
                "address": "10.226.224.52",
                "mask": 29
            }
            ],
            "ipv6address": []                        IPv6 addresses - multiple addresses possible
        },
        "net_provider": "Vodafone CZ",               network provide name
        "net_registration": "registered",            network registration status
        "sim_status": "ready",                       SIM status
        "sim_imsi": "230030159802559",               SIM IMSI - International Mobile Subscriber Identity
```
  </details>


  <details><summary>Modem information - signal </summary>

<blockquote>
  <details><summary>General signal information</summary>

Summary information about mobile network connection.


``` JSON
      "sig_type": "LTE",                             Connected network mode
      "sig_mimo": {                                  MIMO allocation
        "mimo_lte": "1x1 SISO",                      LTE channels configuration
        "mimo_5gnr": "none"                          5G channels configuration
      },
      "sig_rsrq": -12,                               RSRQ - Reference Signal Received Quality [dB]
      "sig_rsrp": -87,                               RSRP - Reference Signal Received Power [dBm]
      "sig_snr": 11.6,                               SNR - Signal to Noise Ratio [dB]
      "sig_rssi": -57,                               RSSI - Received Signal Strength Indicator [dBm]
      "sig_band_class": "eutran-3",                  Band Class
      "sig_channel": 1849,                           Channel
      "net_cell_id": "695297",                       Cell ID
      "net_mcc": 230,                                MCC - Mobile Country Codes
      "net_mnc": 3,                                  MNC - Mobile Network Code
      "net_ltrac": 38500,                            Location Area Code/Tracking Area Code (LAC/TAC)
```
  </details>

<details><summary>Detailed mobile technology information</summary>

The following section may contain the information depending on the mobile network technology used - **sig_type**.

  <details><summary>Detailed LTE information</summary>

``` JSON
        "lte": [                                      LTE info
            {
            "tac": "9664",                            TAC - Tracking Area Code
            "pwr": -56,                               PWR - TX Power [dBm]
            "drx": 640,                               DRX - Discontinuous Reception
            "id": "00A9C01",                          ID
            "earfcn": 1849,                           E-UTRA Absolute Radio Frequency Channel Number 
            "netname": "Vodafone CZ",                 Network Name
            "rsrq": -12,                              RSRQ - Reference Signal Received Quality [dB]
            "rsrp": -89                               RSRP - Reference Signal Received Power [dBm]
            }
        ],
```
  </details>


  <details><summary>Detailed 5G_SA information</summary>

``` JSON
        "_5g_sa": [                                   5G SA Info
            {
            "tac": "9664",                            TAC - Tracking Area Code
            "pwr": -56,                               PWR - TX Power [dBm]
            "drx": 640,                               DRX - Discontinuous Reception
            "id": "00A9C01",                          ID
            "earfcn": 1849,                           E-UTRA Absolute Radio Frequency Channel Number
            "netname": "Vodafone CZ",                 Network Name
            "rsrq": -12,                              RSRQ - Reference Signal Received Quality [dB]
            "rsrp": -89                               RSRP - Reference Signal Received Power [dBm]
            }
        ],
```
  </details>

  <details><summary>Detailed 5G_NSA information</summary>

``` JSON
        "_5g_nsa": [                                   5G NSA Info
          {
          "tac": "94CF",                              TAC - Tracking Area Code
          "pwr": -63,                                 PWR - TX Power [dBm]
          "drx": 640,                                 DRX - Discontinuous Reception
          "id": "002FD04",                            ID
          "earfcn": 1849,                             E-UTRA Absolute Radio Frequency Channel Number
          "netname": "Vodafone CZ",                   Network Name
          "rsrq": -14,                                RSRQ - Reference Signal Received Quality [dB]
          "nr_band": 28,                              Band
          "nr_bandwidth": 10,                         Bandwidth
          "nr_channel": 156030,                       Channel
          "nr_dl_mod": "BPSK",                        Downlink modulation
          "nr_pci": 307,                              PCI
          "nr_rsrp": -101,                            RSRP - Reference Signal Received Power [dBm]
          "nr_rsrq": -20,                             RSRQ - Reference Signal Received Quality [dB]
          "nr_sinr": 12,                              SINR - Signal to Interference plus Noise Ratio [dB]
          "nr_rssi": -79,                             RSSI - Received Signal Strength Indicator [dBm]
          "nr_state": "connected",                    Status
          "nr_txpwr": 0,                              TX Power [dBm]
          "nr_ul_bandwidth": 10,                      UpLink Bandwidth
          "nr_ul_channel": 145030,                    UpLink Channel
          "nr_ul_mod": "BPSK",                        UpLink Modulation
          "rsrp": -101                                RSRP - Reference Signal Received Power [dBm]
        }
        ],
```
  </details>

  <details><summary>LTE Carrier Aggregation details</summary>

The number of items depends on a number of activated LTE carriers.

``` JSON
        "lte_ca": [                                   LTE CA Info
        {
          "lte_ca_index": 1,                          CA Index
          "lte_ca_downlink_modulation": "BPSK",       DownLink Modulation        
          "lte_ca_uplink_modulation": "BPSK",         UpLink Modulation
          "lte_ca_rx_channel": 1849,                  RX Channel
          "lte_ca_tx_power": 0,                       TX Power [dBm] (Primary CA only)
          "lte_ca_band_class": "3",                   Band Class
          "lte_ca_dl_bw": 20,                         Downlink Bandwidth
          "lte_ca_pci": 32,                           PCI - Physical Cell Identity
          "lte_ca_rsrp": -89,                         RSRP - Reference Signal Received Power [dBm]
          "lte_ca_rsrq": -12,                         RSRQ - Reference Signal Received Quality [dB]
          "lte_ca_rssi": -56,                         RSSI - Received Signal Strength Indication [dBm]
          "lte_ca_sinr": 9,                           SINR - Signal to Interference plus Noise Ratio [dB]
          "lte_ca_tac": "9664",                       TAC - Tracking Area Code
          "lte_ca_state": "active"                    CA State
        },
        {
          "lte_ca_index": 2,
          "lte_ca_downlink_modulation": "BPSK",
          "lte_ca_uplink_modulation": "BPSK",
          "lte_ca_rx_channel": 0,
          "lte_ca_band_class": "unknown",
          "lte_ca_dl_bw": 1.4,
          "lte_ca_pci": 0,
          "lte_ca_rsrp": 0,
          "lte_ca_rsrq": 0,
          "lte_ca_rssi": 0,
          "lte_ca_sinr": -20,
          "lte_ca_tac": "",
          "lte_ca_state": "init"
        },
        {
          "lte_ca_index": 3,
          "lte_ca_downlink_modulation": "BPSK",
          "lte_ca_uplink_modulation": "BPSK",
          "lte_ca_rx_channel": 0,
          "lte_ca_band_class": "unknown",
          "lte_ca_dl_bw": 1.4,
          "lte_ca_pci": 0,
          "lte_ca_rsrp": 0,
          "lte_ca_rsrq": 0,
          "lte_ca_rssi": 0,
          "lte_ca_sinr": -20,
          "lte_ca_tac": "",
          "lte_ca_state": "init"
        },
        {
          "lte_ca_index": 4,
          "lte_ca_downlink_modulation": "BPSK",
          "lte_ca_uplink_modulation": "BPSK",
          "lte_ca_rx_channel": 0,
          "lte_ca_band_class": "unknown",
          "lte_ca_dl_bw": 1.4,
          "lte_ca_pci": 0,
          "lte_ca_rsrp": 0,
          "lte_ca_rsrq": 0,
          "lte_ca_rssi": 0,
          "lte_ca_sinr": -20,
          "lte_ca_tac": "",
          "lte_ca_state": "init"
        },
        {
          "lte_ca_index": 5,
          "lte_ca_downlink_modulation": "BPSK",
          "lte_ca_uplink_modulation": "BPSK",
          "lte_ca_rx_channel": 0,
          "lte_ca_band_class": "unknown",
          "lte_ca_dl_bw": 1.4,
          "lte_ca_pci": 0,
          "lte_ca_rsrp": 0,
          "lte_ca_rsrq": 0,
          "lte_ca_rssi": 0,
          "lte_ca_sinr": -20,
          "lte_ca_tac": "",
          "lte_ca_state": "init"
        },
        {
          "lte_ca_index": 6,
          "lte_ca_downlink_modulation": "BPSK",
          "lte_ca_uplink_modulation": "BPSK",
          "lte_ca_rx_channel": 0,
          "lte_ca_band_class": "unknown",
          "lte_ca_dl_bw": 1.4,
          "lte_ca_pci": 0,
          "lte_ca_rsrp": 0,
          "lte_ca_rsrq": 0,
          "lte_ca_rssi": 0,
          "lte_ca_sinr": -20,
          "lte_ca_tac": "",
          "lte_ca_state": "init"
        },
        {
          "lte_ca_index": 7,
          "lte_ca_downlink_modulation": "BPSK",
          "lte_ca_uplink_modulation": "BPSK",
          "lte_ca_rx_channel": 0,
          "lte_ca_band_class": "unknown",
          "lte_ca_dl_bw": 1.4,
          "lte_ca_pci": 0,
          "lte_ca_rsrp": 0,
          "lte_ca_rsrq": 0,
          "lte_ca_rssi": 0,
          "lte_ca_sinr": -20,
          "lte_ca_tac": "",
          "lte_ca_state": "init"
        }
      ],
```
</details>
</details>
</blockquote>
</details>


</blockquote>

</details>




  <details><summary>Measurement data flows details (TCP - multiflow)</summary>

``` JSON
      "tcp_1_TP": 48062326,                             TCP_TestID/(FlowID)     TP - Throughput
      "tcp_1_RTT": 65.25433333333334,                                           RTT - TCP Round Trip Time
      "tcp_1_err_TP": false,                                                    NGA params related evaluation
      "tcp_1_ema_TP": 48062326,                                                 TP - Exponentialy weighted Moving Average
      "tcp_1_err_RTT": false,                                                   NGA params related evaluation
      "tcp_1_ema_RTT": 65.25433333333334,                                       RTT - Exponentialy weighted Moving Average
      "tcp_1/0_err_TP": false,                           subflow 0
      "tcp_1/0_ema_TP": 16242009.136867017,              subflow 0
      "tcp_1/0_err_RTT": false,                          subflow 0
      "tcp_1/0_TP": 16242009.136867017,                  subflow 0
      "tcp_1/0_RTT": 65.825,                             subflow 0
      "tcp_1/0_Retransmits": 0,                          subflow 0
      "tcp_1/0_CWND": 263720,                            subflow 0
      "tcp_1/0_ema_RTT": 65.825,                         subflow 0
      "tcp_1/1_err_TP": false,                           subflow 1
      "tcp_1/1_ema_TP": 15650059.353937814,              subflow 1
      "tcp_1/1_err_RTT": false,                          subflow 1
      "tcp_1/1_TP": 15650059.353937814,                  subflow 1
      "tcp_1/1_RTT": 64.91,                              subflow 1
      "tcp_1/1_Retransmits": 0,                          subflow 1
      "tcp_1/1_CWND": 263720,                            subflow 1
      "tcp_1/1_ema_RTT": 64.91,                          subflow 1
      "tcp_1/2_err_TP": false,                           subflow 2
      "tcp_1/2_ema_TP": 16170258.113302987,              subflow 2
      "tcp_1/2_err_RTT": false,                          subflow 2
      "tcp_1/2_TP": 16170258.113302987,                  subflow 2
      "tcp_1/2_RTT": 65.028,                             subflow 2
      "tcp_1/2_Retransmits": 0,                          subflow 2
      "tcp_1/2_CWND": 263720,                            subflow 2
      "tcp_1/2_ema_RTT": 65.028                          subflow 2
},
```
  </details>


  <details><summary>Measurement data flows details (UDP - multiflow)</summary>

``` JSON
      "udp_1_TP": 6048066,                              UDP_TestID/(FlowID)     TP - Throughput
      "udp_1_err_TP": false,                                                    NGA params related evaluation
      "udp_1_ema_TP": 6048066,                                                  TP - Exponentialy weighted Moving Average
      "udp_1/0_err_TP": false,                                                  NGA params related evaluation
      "udp_1/0_ema_TP": 2016022.2303934467,             subflow 0               TP - Exponentialy weighted Moving Average
      "udp_1/0_TP": 2016022.2303934467,                 subflow 0               TP - Throughput
      "udp_1/0_PLR": 0,                                 subflow 0               Packet Loss Rate
      "udp_1/0_JITTER": 1.3664489436034783,             subflow 0               Jitter
      "udp_1/0_err_PLR": false,                         subflow 0               NGA params related evaluation
      "udp_1/0_err_JITTER": false,                      subflow 0               NGA params related evaluation
      "udp_1/1_err_TP": false,                          subflow 1               NGA params related evaluation
      "udp_1/1_ema_TP": 2016022.2303934467,             subflow 1               TP - Exponentialy weighted Moving Average
      "udp_1/1_TP": 2016022.2303934467,                 subflow 1               TP - Throughput
      "udp_1/1_PLR": 0,                                 subflow 1               Packet Loss Rate
      "udp_1/1_JITTER": 1.445338891564827,              subflow 1               Jitter
      "udp_1/1_err_PLR": false,                         subflow 1               NGA params related evaluation
      "udp_1/1_err_JITTER": false,                      subflow 1               NGA params related evaluation
      "udp_1/2_err_TP": false,                          subflow 2               NGA params related evaluation
      "udp_1/2_ema_TP": 2016022.2303934467,             subflow 2               TP - Exponentialy weighted Moving Average
      "udp_1/2_TP": 2016022.2303934467,                 subflow 2               TP - Throughput
      "udp_1/2_PLR": 0,                                 subflow 2               Packet Loss Rate
      "udp_1/2_JITTER": 1.479250661466545,              subflow 2               Jitter
      "udp_1/2_err_PLR": false,                         subflow 2               NGA params related evaluation
      "udp_1/2_err_JITTER": false                       subflow 2               NGA params related evaluation
```

</details>
  <details><summary>Measurement data flows details (ICMP)</summary>

``` JSON
      "icmp_1_TP": 96000,                                 ICMP_TestID         TP -Throughput
      "icmp_1_RTT": 14.280000000000001,                                       RTT - Round Trip Time
      "icmp_1_PLR": 0,                                                        Packet Loss Rate
      "icmp_1_JITTER": 0.8829985835093795,                                    Jitter
      "icmp_1_ema_TP": 96000,                                                 TP - Exponentialy weighted Moving Average
      "icmp_1_ema_RTT": 14.280000000000001,                                   RTT - Exponentialy weighted Moving Average
      "icmp_1_ema_JITTER": 0.8829985835093795,                                JITTER - Exponentialy weighted Moving Average
      "icmp_1_err_TP": false,                                                 NGA params related evaluation
      "icmp_1_err_RTT": false,                                                NGA params related evaluation
      "icmp_1_err_PLR": false,                                                NGA params related evaluation
      "icmp_1_err_JITTER": false                                              NGA params related evaluation
```
</details>

<details><summary>Measurement data flows details (UDP - Flowping - Interval mode)</summary>

``` JSON
      "udp_2_TP": 2560000,                                UDP_TestID        TP -Throughput
      "udp_2_RTT": 235.81362243749996,                                      RTT - Round Trip Time
      "udp_2_Delay": 162.93965280056,                                       One Way Delay (under developement)
      "udp_2_PLR": 0,                                                       Packet Loss Rate (+ Out Of Order)
      "udp_2_PLR_OOO": 0,                                                   Out Of Order packets
      "udp_2_JITTER": 2.466879,                                             RTT Jitter
      "udp_2_ema_TP": 2560000,                                              TP - Exponentialy weighted Moving Average
      "udp_2_ema_RTT": 235.81362243749996,                                  RTT - Exponentialy weighted Moving Average
      "udp_2_ema_JITTER": 2.466879,                                         JITTER - Exponentialy weighted Moving Average
      "udp_2_err_TP": false,                                                NGA params related evaluation
      "udp_2_err_RTT": false,                                               NGA params related evaluation
      "udp_2_err_PLR": false,                                               NGA params related evaluation
      "udp_2_err_PLR_OOO": false,                                           NGA params related evaluation
      "udp_2_err_JITTER": false                                             NGA params related evaluation
```
</details>
</blockquote>
</blockquote>




# License

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg
