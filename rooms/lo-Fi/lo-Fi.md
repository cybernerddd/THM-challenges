# Tryhackme - LoFi

## Enummeration
Nmap Scan:
- Ports 80(http), 22(ssh) were opened

Used `BurpSuite` to intercept request, repeat it an analyze.
## Exploitation

- Found its vulnerable to LFI(local file Inclusiion)
- Dropped the common payload in repeater `/../../../etc/passwd` -- blocked

later `../../../../../../etc/passwd` -- worked printed /etc/passwd

### Final payload
`../../../../../flag.txt`

## Takeaway
- LFI can be very dangerous if left unchecked
