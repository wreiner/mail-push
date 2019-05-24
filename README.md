# mail-push

Small Python script which checks for new messages in an imap mailbox and notifies via the Pushsafer push notification service. This script is intended to be used as a cronjob or a systemd timer.

## Installation

Deploy the script to a location, e.g. */usr/bin/mail-push* and make it executable:

```
chmod +x /usr/bin/mail-push
```

Create the config file in */etc/mail-push.conf* and set values. An example can be found in *mail-push.conf*. It is a JSON dictionary. Also restrict permissions to the config file as it contains passwords:

```
chmod 400 /etc/mail-push.conf
```

Last create the systemd service and timer by copying the file *mail-push.service* to */etc/systemd/system* and the file *mail-push.timer*:

```
cp mail-push.service /etc/systemd/system
systemctl daemon-reload
systemctl enable reboot-notify.service
```

### Pushsafer Push Notifications

To use the Pushsafer push notification service, download the Pushsafer module from their Github page and copy it to the Python3 module directory, e.g. */usr/lib/python3/dist-packages/pushsafer.py* or use *pip* to install.

Also you may need to install the Python 3 package *requests*, e.g. for Debian systems:

```
apt-get install python3-requests
```

**NOTE** The Pushsafer module does not set a certificate store so there is a warning message displayed when run:

```
/usr/lib/python3/dist-packages/urllib3/connectionpool.py:845: InsecureRequestWarning: Unverified HTTPS request is being made. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warnings
  InsecureRequestWarning)
```

