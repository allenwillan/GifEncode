# GifEncode

# Interest
After working on EmojiObf, I continued to think of other ways to hide in plain sight. While thinking through different social media activities (posting images, watching videos, texting) I was interested to see if there was any space within the GIF specification to hide data. There in fact is a legitimate way to overtly put information within file that is likely not really observed: the "Comment Extension". GIF98a has a number of extension fields that allow various color definitions and playback information. According to the specification:
```
The Comment Extension contains textual information which
is not part of the actual graphics in the GIF Data Stream. It is suitable
for including comments about the graphics, credits, descriptions or any
other type of non-control and non-graphic data. &nbsp;The Comment Extension
may be ignored by the decoder, or it may be saved for later processing;
under no circumstances should a Comment Extension disrupt or interfere
with the processing of the Data Stream.

This block is OPTIONAL; any number of them may appear in the Data Stream.
```

I believe that there may be other ways to hide data within the format (possibly within a custom Application Extension), but experimentation would be needed to see if that data ever gets stripped or causes errors on GIF viewers. This tool uses the "Comment Extension" to hide any number of comments within a GIF file.

# Three Main Ideas
1. Hide in plain site - Similar to emoji, GIFs (mainly in the form of memes) have become intertwined in social media culture. Hiding data within them in a way that doesn't change the overt imagery allows someone to post the GIF somewhat freely.
2. Size - GIF is a loss-less format, and as such many GIF are quite large. I pulled three that I use frequently on Discord and was surprised at the sizes: 401KB, 3.72MB, and 10.6MB. This tool compresses and encrypts the input data, before base64 encoding it (the base64 is required by the GIF format, as it requires 7-bit encoding). Unless you're transferring monster files, it is easy to hide even a few MB in some files without much concern.
3. Portability - The GIF format is universal, and predates the Internet. Although it is arguably a bad format, it's still consistently used and supported on every platform and type of device. This means that the GIF should be viewable and postable anywhere.

# Future Direction
1. Variation - Explore other aspects of the GIF format for other opportunities to abuse the file structure.
2. More obfuscation - Currently the tool chooses a random other extension offset and inserts the Comment Extension structure in there as one block comment. Allowing the user to choose where in the structure would be nice (although not particularly helpful), but what I believe would be more helpful would be to break up the data to insert using a seed, then insert the data across multiple Comment Extension structures across the entire file. This would make retrieve of the data difficult without the seed.
3. Support testing - Testing to ensure that the Comment Extensions don't get stripped or flagged anywhere would be ideal. It at the least works through Giphy hosting as well as simply sending via Discord.

# Resources
* https://youtu.be/w4FuIviJJ6o - Overview video
* https://www.w3.org/Graphics/GIF/spec-gif89a.txt - The specification for GIF89a, which was used to build the parser
* https://www.fileformat.info/format/gif/egff.htm - Useful information about the GIF format, to include some helpful images
* https://giflib.sourceforge.net/whatsinagif/bits_and_bytes.html - A helpful breakdown of some aspects of the GIF format
