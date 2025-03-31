# path-finder | medium
(under construction)

## description
The map with some weird objects stored on a USB flash drive was revealed in one of the New York City's sewage systems...Who left it there? Does it relate to a recent crime on one of NY streets? Or it might be even worse...it was carried through a sewage for miles. Anyway, this is your turn to discover the hidden message. <br>
hint: Base64 encoded

## category
- forensics

## knowledge / tools used
- basic linux command line knowledge
- ``steghide``
- ``xxd`` or ``hexdump``, ``hexedit``, really anything you can use to read and edit hex dumps
- base64 decoder

## flag
jctfv{n01r_cr1m3_4mb1guity_isol4ti0n}

## credit
[Malanka](https://github.com/malanka228)

## solution steps

1. after unzipping path-finder.zip, you'll find five files: ``MAP.jpg``, ``m.jpg``, ``palms.jpg``, ``s.mp3``, and ``t.jpg``.
2. ``MAP.jpg`` shows you how to piece the flag together. that, along with the hint being "Base64 encoded," it's likely that you'll be looking for a base64 string from each file.
3. starting with ``palms.jpg``. i check the filetype to make sure that it has the correct extension, which it does. you can then move on to trying other commands, like passing ``palms.jpg`` to ``strings`` or ``exiftool``. both of these show a base64 string in the ``Author`` field, and when decoded, gives you the first part of the flag.
4. the map then shows a mountain, which is referring to ``m.jpg``. putting it through ``steghide extract -sf m.jpg`` gives you the next part of the flag.
5. the next part is the ship, which is ``s.mp3``. i first tried opening it and it wouldn't play any music. this led me to check the filetype, and it turns out that it's actually a jpeg file, not an mp3. renaming ``s.mp3`` to ``s.jpg`` allows you to open it, which then reveals an image of a ship with a base64 string.
6. the last part is the treasure chest: ``t.jpg``. we run into a similar problem, as ``t.jpg`` cannot be displayed because it contains errors. checking its filetype with ``file`` will just return data, which happens when a specific file type can't be determined, so it's classified as generic binary data. there are three reasons for why this can happen: (1) the file lacks a recognizable header, (2) it's encrypted or compressed in an unknown way, or (3) it's just raw binary data. we can check if the file has a header with ``hexdump -C t.jpg | head`` or ``xxd t.jpg | head``. the first 12 bytes are ``00``, which are null bytes -- empty data. you can compare the headers of the other jpg files and see that they all have the same header of ``ff d9 ff e0 00 ...``, or you can look up what the header is for JFIF files. editing ``t.jpg``'s hex dump with a hex editor like ``hexedit`` and writing the proper jpg header will allow you to open the image and get the final part of the string.
