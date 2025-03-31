# path-finder | medium

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
