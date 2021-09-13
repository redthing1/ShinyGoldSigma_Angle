# rom analysis

## finding data tables

often in hacked roms, you want to find data tables for things like items or pokemon.

within mainline gen iii roms, the offsets are known. you can use that to look at the data in that offset, to get an idea of what data is there.
for example, with the item table, the offset for the gen iii firered item table within the rom is known. at that offset we'll find all the item entries.

the entry `0x01` is the entry for the `MASTER BALL`. since nearly all romhacks keep the main engine data structures intact, we can search for the same table within a hacked rom for simply searching for that item we have chosen.

so we'd search the rom for the (PokeString encoded) data for `MASTER BALL`. Often if capitalization is modified, you also want to try variations like `Master Ball`. Also, sometimes parts of the data like the space character can be different, so maybe try searching for many different strings or just parts of one. Overall you just want to correlate where all the items appear together to find the item table.

### example

searching for `Master Ball`
```
xxd -u -c 256 -g 1 PokemonSGS_v1.3.8.gba | grep 'C7 D5 E7 E8 D9 E6 00 BC D5 E0 E0 FF 00 00 01'
```