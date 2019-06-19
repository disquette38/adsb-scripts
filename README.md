# adsb-wiki
Solutions to common problems using dump1090 variants and ADS-B feeders


## 1. Install script for dump1090-fa

- automatically reconfigures fr24feed (if installed)
- fixes read-only problem with pi24 image
- installs dump1090-fa
- makes it possible to change gain without editing a file

To use the install script, just paste or enter the following command:
```
sudo bash -c "$(wget -O - https://raw.githubusercontent.com/wiedehopf/adsb-wiki/master/install-dump1090-fa.sh)"
```

-----

### 1.1 Change gain with provided helper:

Command:
```
sudo dump1090-fa-gain 42.1
```


Available gain settings:
```
0.0 0.9 1.4 2.7 3.7 7.7 8.7 12.5 14.4 15.7 16.6 19.7 20.7 22.9 25.4
28.0 29.7 32.8 33.8 36.4 37.2 38.6 40.2 42.1 43.4 43.9 44.5 48.0 49.6 -10
```
(-10 is a special setting which in practice equals a gain of around 55)

---

### 1.2 Configure dump1090-fa location

See the explanation here:
https://github.com/wiedehopf/adsb-wiki/wiki/Installing-dump1090-fa#4-configuring-dump1090-fa-location

## 2. Automatic gain adjustment for dump1090-fa

- only for rtl-sdr/DVB-T USB receiver, not Airspy or Beast receivers
- at 2:45 in the morning, the gain is changed and dump1090-fa restarted
- changes gain by one step every night, only if required
- uses "strong signals" to determine if gain should be changed
- if the percentage of strong signals is greater than 5 percent -> gain is reduced
- if the percentage of strong signals is less than 1 percent -> gain is increased
- thresholds adjustable in /etc/default/dump1090-fa-autogain

#### Installation:

```
sudo bash -c "$(wget -O - https://raw.githubusercontent.com/wiedehopf/adsb-wiki/master/dump1090-fa-autogain.sh)"
```

#### Removal / Deinstallation:

```
sudo rm /etc/cron.d/dump1090-fa-autogain
```

