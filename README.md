# justc-envdir

This is a quick and dirty fork of the [s6-envdir](https://skarnet.org/software/s6/s6-envdir.html) program.

Differences between this version and `s6-envdir`:

| `justc-envdir` | `s6-envdir` |
|------------------------------|
| Reads the entire file into the environment. | Truncates at 4095 bytes. |
| Allows setting empty environment variables with empty files. | Removes environment variables on empty files. |
| Does not transform `NULL` bytes, terminates variable at first `NULL` byte. | Transforms `NULL` bytes. |

You will need to to take your own precautions around maximum file sizes.

## Usage

`justc-envdir [ -I | -i ] dir prog...`

* justc-envdir reads files in *dir*. For every file *f* in *dir*, that does not begin with a dot and does not contain the `=` character:
    * Add a variable named *f* to the environment (or replace *f* if it already exists) with the contents of the file *f* as value. The file is read verbatim, if the file contains a `NULL`, the value is terminated at that byte.

## Options

* `-i` : strict. If *dir* does not exist, exit 111 with an error message. This is the default.
* `-I` : loose. If *dir* does not exist, exec into *prog* without modifying the environment first.

## LICENSE

ISC - see `LICENSE.md`
