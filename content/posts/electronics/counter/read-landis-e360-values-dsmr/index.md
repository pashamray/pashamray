+++
title = "Read values from Landis + Gyr E360 SMR 5.0 by DSMR"
date = 2025-08-31T11:55:00+01:00
authors = ["pashamray"]
description = "Read values from Landis Gyr E360 CDMA"
tags = ["Landis", "E360", "dsmr", "log"]
draft=false
+++

# Hardware

## Counter

[short doc](docs/handleiding-landis-gyr-e360-smr-5.pdf)

![counter](https://eu.landisgyr.com/hs-fs/hubfs/EMEA/EUW_2016/e360-2.png?width=600&name=e360-2.png)
*img from: https://eu.landisgyr.com/blog/european-utility-week-2016/advanced-metering-infrastructure/e360*

Counter has P1 port for read parameters by DSMR protocol 


## UART FTDI Adapter for connect to P1 port

I buy [adapler on aliexpress](https://nl.aliexpress.com/item/1005001747429524.html?spm=a2g0o.order_list.order_list_main.5.327c1802sG9KVX&gatewayAdapt=glo2nld)

![adapter](img/adapter.png)

# Software

## Library
I use https://github.com/ndokter/dsmr_parser library for read values and use example from README

### Example
```python
from dsmr_parser import telegram_specifications
from dsmr_parser.clients import SerialReader, SERIAL_SETTINGS_V5

serial_reader = SerialReader(
    device='/dev/ttyUSB0',
    serial_settings=SERIAL_SETTINGS_V5,
    telegram_specification=telegram_specifications.V5
)

for telegram in serial_reader.read():
    print(telegram)  # see 'Telegram object' docs below
```


run it and get log in telegram format

```txt
P1_MESSAGE_HEADER: 	 50	[None]
P1_MESSAGE_TIMESTAMP: 	 2025-08-30T16:33:58+00:00	[None]
EQUIPMENT_IDENTIFIER: 	 45303035313030353533363736********	[None]
ELECTRICITY_USED_TARIFF_1: 	 4400.065	[kWh]
ELECTRICITY_USED_TARIFF_2: 	 3889.624	[kWh]
ELECTRICITY_DELIVERED_TARIFF_1: 	 3714.178	[kWh]
ELECTRICITY_DELIVERED_TARIFF_2: 	 8656.318	[kWh]
ELECTRICITY_ACTIVE_TARIFF: 	 0001	[None]
CURRENT_ELECTRICITY_USAGE: 	 0.026	[kW]
CURRENT_ELECTRICITY_DELIVERY: 	 0.000	[kW]
LONG_POWER_FAILURE_COUNT: 	 2	[None]
SHORT_POWER_FAILURE_COUNT: 	 16	[None]
POWER_EVENT_FAILURE_LOG: 	 	 buffer length: 1
	 buffer type: 0-0:96.7.19
	 event occured at: 2020-01-01T08:15:55+00:00	 for: 1599 [s]
VOLTAGE_SAG_L1_COUNT: 	 20	[None]
VOLTAGE_SWELL_L1_COUNT: 	 2	[None]
INSTANTANEOUS_VOLTAGE_L1: 	 229.9	[V]
INSTANTANEOUS_CURRENT_L1: 	 1	[A]
TEXT_MESSAGE: 	 None	[None]
INSTANTANEOUS_ACTIVE_POWER_L1_POSITIVE: 	 0.026	[kW]
INSTANTANEOUS_ACTIVE_POWER_L1_NEGATIVE: 	 0.000	[kW]
MBUS DEVICE (channel 1)
	MBUS_DEVICE_TYPE: 	 3	[None]
	MBUS_EQUIPMENT_IDENTIFIER: 	 47303036343030323031373031********	[None]
	MBUS_METER_READING: 	 3333.555	[m3] at 2025-08-30T16:30:08+00:00
```

You can get single values or units:
```python
# Print contents of all available values
# See dsmr_parser.obis_name_mapping for all readable telegram values.
# The available values differ per DSMR version and meter.
print(telegram)
# P1_MESSAGE_HEADER:                42 [None]
# P1_MESSAGE_TIMESTAMP:         2016-11-13 19:57:57+00:00 [None]
# EQUIPMENT_IDENTIFIER:         3960221976967177082151037881335713 [None]
# ELECTRICITY_USED_TARIFF_1:    1581.123 [kWh]
# etc.

# Example to get current electricity usage
print(telegram.CURRENT_ELECTRICITY_USAGE)  # <dsmr_parser.objects.CosemObject at 0x7f5e98ae5ac8>
print(telegram.CURRENT_ELECTRICITY_USAGE.value)  # Decimal('2.027')
print(telegram.CURRENT_ELECTRICITY_USAGE.unit)  # 'kW'

# All Mbus device readings like gas meters and water meters can be retrieved as follows. This
# returns a list of MbusDevice objects:
mbus_devices = telegram.MBUS_DEVICES

# A specific MbusDevice based on the channel it's connected to, can be retrieved as follows:
mbus_device = telegram.get_mbus_device_by_channel(1)
print(mbus_device.MBUS_DEVICE_TYPE.value)  # 3
print(mbus_device.MBUS_EQUIPMENT_IDENTIFIER.value)  # '4730303339303031393336393930363139'
print(mbus_device.MBUS_METER_READING.value)  # Decimal('246.138')
print(mbus_device.MBUS_METER_READING.unit)  # m3

# DEPRECATED: the dictionary approach of getting the values by key or `.items()' or '.get() is deprecated
telegram[obis_references.CURRENT_ELECTRICITY_USAGE]
```

### My script

```python
from dsmr_parser import telegram_specifications
from dsmr_parser.clients import SerialReader, SERIAL_SETTINGS_V5

serial_reader = SerialReader(
    device='/dev/ttyUSB0',
    serial_settings=SERIAL_SETTINGS_V5,
    telegram_specification=telegram_specifications.V5
)

for telegram in serial_reader.read():
    # Example to get current electricity usage
    # print(telegram)  # <dsmr_parser.objects.CosemObject at 0x7f5e98ae5ac8>
    print(telegram.CURRENT_ELECTRICITY_USAGE.value)  # Decimal('2.027')
    print(telegram.CURRENT_ELECTRICITY_USAGE.unit)  # 'kW'

    print(telegram.CURRENT_ELECTRICITY_DELIVERY.value)  # Decimal('2.027')
    print(telegram.CURRENT_ELECTRICITY_DELIVERY.unit)  # 'kW'

    # All Mbus device readings like gas meters and water meters can be retrieved as follows. This
    # returns a list of MbusDevice objects:
    # mbus_devices = telegram.MBUS_DEVICES

    # A specific MbusDevice based on the channel it's connected to, can be retrieved as follows:
    mbus_device = telegram.get_mbus_device_by_channel(1)
    #print(mbus_device.MBUS_DEVICE_TYPE.value)  # 3
    #print(mbus_device.MBUS_EQUIPMENT_IDENTIFIER.value)  # '4730303339303031393336393930363139'
    print(mbus_device.MBUS_METER_READING.value)  # Decimal('246.138')
    print(mbus_device.MBUS_METER_READING.unit)
```

```txt
0.000
kW
0.630
kW
3229.407
m3
```

### References

- https://github.com/ndokter/dsmr_parser
- https://github.com/dsmrreader/dsmr-reader
- https://www.home-assistant.io/integrations/dsmr/
- https://eu.landisgyr.com/blog/european-utility-week-2016/advanced-metering-infrastructure/e360
