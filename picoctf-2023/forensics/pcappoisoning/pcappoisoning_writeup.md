# PicoCTF 2023 Forensics Writeup: PcapPoisoning

## Downloading the Files
First, we download the required files using `wget`:

```bash
wget https://artifacts.picoctf.net/c/377/trace.pcap
```

## Open the file using wireshark

Let's open `trace.pcap` using Wireshark
```bash
wireshark trace.pcap
```

## Examine the packets

Looking at a glance we can see that most of the packets with the protocol of `FTP-DATA` are all transmitting the same data but let's just apply a filter to find any packets that would contain the string `picoCTF`

![](/screenshots/filter.png)

## Retrieving the flag
It seems that wireshark found a packet containing the string `picoCTF` in it! Let's open the packet!

![](/screenshots/flag.png)

Great! We found the flag!
