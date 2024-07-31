# PicoCTF 2023 Forensics Writeup: FindAndOpen

## Downloading the Files
First, we download the required files using `wget`:

```bash
wget https://artifacts.picoctf.net/c/494/flag.zip
wget https://artifacts.picoctf.net/c/494/dump.pcap
```

## Inspecting the Zip File
It seems that the flag is hidden inside the zip file. Let's try unzipping it:

```bash
unzip flag.zip
```

**Output:**
```
Archive:  flag.zip
[flag.zip] flag password:
```

The zip file is password-protected. PicoCTF's rules prohibit password brute-forcing, so we'll need to find the password from the provided `dump.pcap` file.

## Analyzing the PCAP File
Let's open the `dump.pcap` file using Wireshark:

```bash
wireshark dump.pcap
```

## Examining Packets in Wireshark
Upon examining the packets, we notice the following:

### Packets 1 to 9
```
Flying on Ethernet secret: Is this the flag 
```
The data in these packets hints that the flag is transmitted over Ethernet.

### Packets 23 to 47
```
iBwaWNvQ1RGe1Could the flag have been split?
```
The string "iBwaWNvQ1RGe1" appears to be encoded or a hash.

### Packet 48
```
AABBHHPJGTFRLKVGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8=
```
This looks like Base64 encoded data. Let's decode it:

```bash
echo -n "AABBHHPJGTFRLKVGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8=" | base64 -d
```

**Output:**
```
This is the secret: picoCTF{R34DING_LOKd_
```

## Continuing the Analysis
We have part of the flag, but it seems incomplete. Let's continue examining the packets.

### Packets 49 to 57
```
bababkjaASKBKSBACVVAVSDDSSSSDSKJBJS
```
This appears to be gibberish.

### Packets 58 to 65
```
Maybe try checking the other file
```
This suggests we should revisit the `flag.zip` file.

## Unzipping with the Password
We will now try unzipping the `flag.zip` file using the partial flag as the password:

```bash
unzip flag.zip
```

**Input:**
```
[flag.zip] flag password: picoCTF{R34DING_LOKd_
```

**Output:**
```
Archive:  flag.zip
 extracting: flag
```

## Retrieving the Final Flag
Finally, let's read the contents of the extracted `flag` file:

```bash
cat flag
```

**Output:**
```
picoCTF{R34DING_LOKd_fil56_succ3ss_b98dda6a}
```

## Conclusion
We successfully retrieved the flag: `picoCTF{R34DING_LOKd_fil56_succ3ss_b98dda6a}`.
```
