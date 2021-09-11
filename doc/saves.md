
# save rev eng

+ two save slots, 14 sections each. the signature `25 20 01 08` appears 28 times as expected
+ my character's name is `Beans`, encoded as `BC D9 D5 E2 E7`, using this i can find the start of Section 0
+ which slot is active? right after the signature a 4-byte field says the save index. highest is most recent. all sections have one, make sure they match
+ looks like there's a blank section(s) at the start?
    + assuming active slot is the first one
    + player name appears in a weird section, can't modify without breaking cksum
    + at `0x2000` i see the player name in a format that actually matches docs. this section appears to be player data and goes from `0x2000` to `0x2FFF`

## resources
+ https://m.bulbapedia.bulbagarden.net/wiki/Save_data_structure_(Generation_III)
+ https://m.bulbapedia.bulbagarden.net/wiki/Character_encoding_(Generation_III)