# bible-search

A small Perl wrapper around [diatheke](https://www.crosswire.org/sword/diatheke/) that prints the full text of every verse matching a search.

`diatheke -s phrase` only returns a list of references, and it glues the first two references together (`Genesis 15:1Genesis 21:17`). This script parses that list, looks each verse up, and prints the text.

## Requirements

- Perl 5
- [diatheke](https://www.crosswire.org/sword/diatheke/) (from the SWORD project)
- At least one installed SWORD Bible module

On Debian or Ubuntu:

```bash
sudo apt install libsword-utils
```

Install a module with `installmgr`, or copy it into `~/.sword/`. The default module is **FinRK** (Raamattu Kansalle 2012). List what you have with:

```bash
diatheke -b system -k modulelist
```

## Install

```bash
chmod +x diasearch
sudo cp diasearch /usr/local/bin/
```

Or run it from this directory with `./diasearch`.

## Usage

```text
diasearch [-b module] [-s type] [-r range] [-m max] search phrase
```

| Option | Meaning |
| --- | --- |
| `-b module` | SWORD module. Default: `FinRK` |
| `-s type` | Search type: `phrase` (default), `regex`, or `multiword` |
| `-r range` | Limit the search, for example `John` or `Mt-Jn` |
| `-m max` | Maximum number of hits to retrieve |

```bash
diasearch do not fear
diasearch -r John eternal life
diasearch -b AKJV -s multiword grace faith
```

Example (`diasearch -r John love`):

```text
2 verses in FinRK for "rakkaus":

John 13:35: Siitä kaikki tuntevat teidät minun opetuslapsikseni, että teillä on keskinäinen rakkaus.”
John 17:26: Minä olen tehnyt sinun nimesi heille tunnetuksi ja teen vastakin, että se rakkaus, jolla sinä olet rakastanut minua, olisi heissä ja minä olisin heissä.”
```

If nothing matches, the script prints `No matches in FinRK for "..."` and exits 0.
