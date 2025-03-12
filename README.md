# star

star is a CLI tool that allows you to bookmark your favorite folders and instantly navigate to them.

## Requirements

This software has been developed on bash >= 5.2, untested on prior versions (pretty sure it does not work on bash 3).
It uses GNU tools such as `find`, `basename`, which are not always the default (e.g. find exists on MacOS, but does not have the same options as the GNU version).

On MacOS, GNU utils can be installed using brew: https://apple.stackexchange.com/questions/69223/how-to-replace-mac-os-x-utilities-with-gnu-core-utilities.

## Installation

Clone the repo and source the file [`star.sh`](./star.sh):
```bash
git clone https://github.com/Fruchix/star.git
cd star
source star.sh
```

Also source the file in your `.bashrc`:
```
echo "source $(pwd)/star.sh" >> ~/.bashrc
```
or `.zshrc`:
```
echo "source $(pwd)/star.sh" >> ~/.zshrc
```


## Usage

```
star [OPTION [ARGUMENTS...]]
```
Without arguments:
- Show this help message.

With `OPTION`:
- Will execute the feature associated with this option.
- `OPTION` can be one of `add`, `list`, `load`, `rename`, `remove`, `reset`, `help`, or one of their shortnames (such as `-h` for `help`). Use `star help` for more information on short parameters and aliases.

---
```
star add [NAME]
```
Add the current directory to the list of starred directories.
The new star will be named after `NAME` if provided, otherwise it will use the basename of the current directory.
`NAME` must be unique (among all stars).
`NAME` can contain slashes `/`.

---
```
star list
sL
```
List all starred directories, sorted according to last load (top ones are the last loaded stars).

---
```
star load [star]
sl
```
Navigate (cd) into the specified [star] directory.
If no argument is provided, it displays the list of starred directories (same behavior as star list).

`[star]` should be the name of a starred directory (one that is listed using "star list").

> Also updates the last accessed time (used to sort stars when listing them).
---
```
star rename <existing star> <new star name>
```
Rename an existing star.

---
```
star remove <star> [star] [star] [...]
```
Remove one or more starred directories.

`<star>` should be the name of a starred directory.

---
```
star reset [-f|--force]
```
Remove the ".star" directory (thus remove the starred directories).
The argument -f or --force will force the reset without prompting the user.

---
```
star help
```
Get more information.

## Faster Usage

> Use `star help` for all options and aliases.

The following aliases are provided to make your life easier:
- `sah` = star add
- `sL` = star list
- `sl` = star load (which is the same as "star list" when no argument is provided)
- `unstar` = star remove
- `srm` = star remove

## Example

```bash
fruchix@debian:~/Documents/star$ star list
No ".star" directory (will be created when adding new starred directories).

fruchix@debian:~/Documents/star$ star add
Added new starred directory: star -> /home/fruchix/Documents/star

fruchix@debian:~/Documents/star$ star list
star  ->  /home/fruchix/Documents/star

fruchix@debian:~/Documents/star$ cd ..

fruchix@debian:~/Documents$ star add my/docs
Added new starred directory: my/docs -> /home/fruchix/Documents

fruchix@debian:~/Documents$ sl
my/docs  ->  /home/fruchix/Documents
star     ->  /home/fruchix/Documents/star

fruchix@debian:~/Documents$ cd

fruchix@debian:~$ sl star

fruchix@debian:~/Documents/star$ sl my/docs

fruchix@debian:~/Documents$ unstar my/docs
Removed starred directory: my/docs
```

## License

[Apache](./LICENSE)  
> Copyright 2024 Fruchix
