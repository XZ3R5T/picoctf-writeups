# PicoCTF 2023 Forensics Writeup: hideme

## Downloading the Files
First, we download the required files using `wget`:

```bash
wget https://artifacts.picoctf.net/c/259/flag.png
```

## Inspecting the flag.png
It seems that the flag is hidden inside this PNG lets try and open it as an image:

```bash
xdg-open flag.png
```

**Output:**
![](/screenshots/preview-screenshot.png)

As we thought there's nothing we could get from opening it as is

## Searching binary images for embedded files and executable code
Let's try looking for any embedded files inside the png:

```bash
binwalk flag.png
```

**Output:**
![](/screenshots/binwalk_output-screenshot.png)

Upon examining the output, we notice that it has a directory called `secret/` and it contains `secret/flag.png`

## Extracting the file
After we saw that there's a file named `flag.png`, we just need to extract it

```bash
binwalk -e flag.png
```
**Output:**
```
_flag.png.extracted
```

## Retrieving the Flag and Conclusion
Now that we have extracted the directory we just need to open up the flag

```bash
xdg-open _flag.png.extracted/secret/flag.png
```
**Output:**
![](/screenshots/flag-screenshot.png)

Well thats the flag, wasn't so hard ey?

