# Query a Device from CMS (API)

This queries allow you to retrieve the data of a managed device through cerntral management system (CMS). The queries are redirected by CMS helps to reduce time and repetitive commands. Use the scripting language of your choice to store device serial numbers and use them to issue a query to several devices.

## Step 1. Get a list of devices

Retrieve a list of devices that CMS manages:

```
https://cms-ip/api/?type=redirect&cmd=<show><devices><connected></connected></devices></show>
```

The response includes the SN (serial number) of each device connected. The response has a <serial> XML element for each device.

```
<response status="success">
    <result>
        <devices name="007200002517">
            <serial>007200005243</serial>
            <connected>yes</connected>
            <unsupported-version>no</unsupported-version>
            <deactivated>no</deactivated>
            <hostname>HS-6-1-VM</hostname>
            <ip-address>10.4.3.137</ip-address>
            <uptime>81 days, 20:39:41</uptime>
            <family>vm</family>
            <model>HS-StoneOS-E</model>
            <sw-version>5.0R4.1.3</sw-version>
            <app-version>555-3129</app-version>
            <av-version>2254-2693</av-version>
            <threat-version>555-3129</threat-version>
            <url-filtering-version>2016.02.02.416</url-filtering-version>
            <logdb-version>6.1.3</logdb-version>
<!--truncated -->
        </devices>
    </result>
</response>

```


## Step2. Store device serial number

In your code, store the device serial numbers (SN) returned in the response to the previous request.

## Step 3. Query one device

A normal request to show system information on a device looks like this:
```
https://device-ip/api/?type=normal&cmd=<show><system><info></info></system></show>
```

To directly target a device through CMS, add the firewall serial number to the request:
```
https://cms-ip/api/?type=redirect&cmd=<show><system><info></info></system></show>&target=device-sn
```
A successful response should look like this:

```
<response status="success">
    <result>
        <system>
            <hostname>firewall</hostname>
            <ip-address>10.40.0.3</ip-address>
            <netmask>255.255.224.0</netmask>
            <default-gateway>10.41.0.1</default-gateway>
            <is-dhcp>no</is-dhcp>
            <ipv6-address>unknown</ipv6-address>
            <ipv6-link-local-address>fe80::21c:17cf:feff:c04a/64</ipv6-link-local-address>
            <ipv6-default-gateway></ipv6-default-gateway>
            <mac-address>00:1b:17:fc:c0:4a</mac-address>
            <time>Tue Apr 16 13:39:09 2016</time>
            <uptime>12 days, 0:05:26</uptime>
            <devicename>pm-firewall</devicename>
            <family>E</family>
            <model>HS-E2100</model>
            <serial>001802000104</serial>
            <sw-version>5.0R4.1.0-c54</sw-version>
            <app-version>537-2965</app-version>
            <app-release-date>2016/04/16 18:10:48</app-release-date>
            <av-version>2149-2586</av-version>
            <av-release-date>2016/04/16 15:31:55</av-release-date>
            <threat-version>537-2965</threat-version>
            <threat-release-date>2016/04/16 18:10:48</threat-release-date>
            <url-filtering-version>2016.04.16.226</url-filtering-version>
            <logdb-version>7.0.9</logdb-version>
            <platform-family>E-Series</platform-family>
            <vpn-disable-mode>off</vpn-disable-mode>
            <multi-vsys>on</multi-vsys>
            <operational-mode>normal</operational-mode>
        </system>
    </result>
</response>
```
Repeat this request for each connected device.
