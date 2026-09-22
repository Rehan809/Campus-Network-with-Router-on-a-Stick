# Troubleshooting Guide

Use a bottom-up approach instead of changing random configurations.

## 1. Physical / interface status

```text
show ip interface brief
```

Check for `up/up`.

## 2. VLAN and access ports

```text
show vlan brief
show interfaces status
```

Confirm each PC is on the intended VLAN.

## 3. Trunk

```text
show interfaces trunk
```

Confirm VLANs 10,20,30,40 are allowed.

## 4. Gateway

From a client, ping its VLAN gateway.

## 5. Inter-VLAN routing

From a client, test another VLAN gateway.

## 6. WAN

```text
ping 10.0.0.2
```

## 7. Default route

```text
show ip route
```

Look for the default route via `10.0.0.2`.

## 8. NAT/PAT

```text
show access-lists
show ip nat translations
show ip nat statistics
```

Generate traffic first, then inspect translations.

## 9. ISP return path

On ISP Router:

```text
show ip route
```

Confirm the four campus networks point to `10.0.0.1`.

## 10. End-to-end

```text
ping 8.8.8.8
```
