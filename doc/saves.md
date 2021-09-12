
# save rev eng

+ two save slots, 14 sections each. the signature `25 20 01 08` appears 28 times as expected
+ my character's name is `Beans`, encoded as `BC D9 D5 E2 E7`, using this i can find the start of Section 0
+ which slot is active? right after the signature a 4-byte field says the save index. highest is most recent. all sections have one, make sure they match
+ looks like there's a blank section(s) at the start?
    + assuming active slot is the first one
    + player name appears in a weird section, can't modify without breaking cksum
    + at `0x2000` i see the player name in a format that actually matches docs. this section appears to be player data and goes from `0x2000` to `0x2FFF`
    + section ids actually seem to be correct, with trainer info being `00 00` and team/item info being `01 00`
+ player info section (`00 00`)
    + player name can be modded (but this is duplicated across the save, probably better to leave)
    + playtime can be modded as expected
+ team/item section (`01 00`)
    + money is a 4-byte field offset `0x290` from the section start. for me, section start was `0x5000`, so this was `0x5290`
    + team size (u32) is at offset `0x0034`, pokemon list starts at `0x0038`
+ confirmed that sgs uses "save block expansion", meaning that it utilizes details of the section layout to enable it to transparently store extra data. here is a brief overview and explanation
    + based on the save data section structure, there are two save slots, and each save slot is composed of 14 sections. these sections are stored on 14 sectors of size `0x1000` (4096).
    + sections are rotated around, so the section number does not match the sector number, but each section should only be appearing once.
    + firered section blocks are `0x1000`, matching sector size. the section consists of a data content of length `0xF80` (3968), and a tail of length `0x80` (128). this tail is composed of an unknown/padding content and then the final 12 bytes are the section footer. 

## resources
+ see the `pdf/` dir for documents
+ https://m.bulbapedia.bulbagarden.net/wiki/Save_data_structure_(Generation_III)
+ https://m.bulbapedia.bulbagarden.net/wiki/Character_encoding_(Generation_III)
