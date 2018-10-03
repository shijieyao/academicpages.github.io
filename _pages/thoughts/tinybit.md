<h2>Python</h2>

<h3>useful pages</h3>

- <...>

<h3>tips</h3>

- removing items while looping lists: the list is being modified, pay attention to the realtime count of elements in the list
  - [**better to use list comprehension**](https://stackoverflow.com/questions/1207406/how-to-remove-items-from-a-list-while-iterating): `l = [n for n in l if n != 1]` to remove elements unequal to 1

- changing the starting index of enumerate: `enumerate(something, 1)` will start indexing from 1

- [**tuple/list comparison**](https://docs.python.org/3/reference/expressions.html#value-comparisons): tuples and lists are compared lexicographically.
  - e.g. `(1, 2) < (2, 1) == True` # as the first tuple _comes_ before the second one
  - e.g. `[2, 3] < [1, 8] == False`

- string split
  - `str.split(sep, maxsplit)`and `str.rsplit(seq, maxsplit)`
  - e.g. `'a,b,c'.split(',', 1) -> ['a', 'b,c']` vs `'a,b,c'.rsplit(',', 1) -> ['a,b', 'c']`, `r` means reverse, so splitting from the end of the string

- paths
  - diff between `sys.path.append(os.path.abspath('path')` and `os.chdir('path')`
  - when `os.chdir`ing inside a func? what would happen to the current directory if that func being called?

- `any()`
  - `True` if at least one element of an iterable is True
  - `False` if all elements are false or if an iterable is empty

- `sys.argv`
  - if multiple consecutive arguments all of the same type, can use `sys.argv[n:]`

- check if file or dir exists
  - [**a very object-oriented approach**](https://stackoverflow.com/questions/82831/how-to-check-whether-a-file-exists)

======================================================================================

<h2>Shell (Bash)</h2>

<h3>useful pages</h3>

- [**use commands and pipes to "mine" and extract data**](http://teaching.idallen.com/cst8207/13w/notes/805_data_mining.html)

- [**`sed`**](https://edoras.sdsu.edu/doc/sed.html)

<h3>tips</h3>

- frequent errors (that I usually make!):
  - extra `|` before `<`, especially at the last line before `<`
  - unlike Python, commands like `a=b=$1` is not allowed, instead, split them as `a=$1; b=$1`
  - confusing use of `$ bash ${file}` and `$ python ${file}`, double check what type of the file is that I'm running

- [rename file/dir etc](https://www.cyberciti.biz/faq/bash-rename-files/)
  - rename a file: `mv ${oldname} ${newname}`

- `mkdir`:
	- `mkdir -p ${dir_name}` will not prompt `mkdir: ${dir_name}: File exists` if already exists

- `bc`:
  - return `0 `or `1`: e.g. `echo "5 > 4 | bc"` returns `1`

- `sed` text replace
  - `sed -i -e 's/few/asd/g' hello.txt` to replace `few` with `asd` in all lines in file `hello.txt`

- combine `cut`, `awk` and `sed` to slice/extract text, often used in text preprocessing (btw Shell is quite ideal for dealing with text)
  - e.g.

      ```
      cut -f ${column_num} ${oldfile} | \
      sed '/^#/ d' > ${newfile}
      ```

     `cut` then extracts the information at the `${column_num}`th column; at the end `sed` `d`eletes all the lines beginning (`^`) with a `#`, and saves the resultant text to `${newfile}`.

- for search, can use `awk`, `sed` or more generally `grep`
  - e.g.

      ```awk '/<something>/' ${file}```

      ```sed -n '/<something>/p' ${file}```

      ```grep 'something' ${file}```

- use `sed` to delete a specific line from a file
  - `sed '1d' ${file}` to remove the first line from the file

- use `awk` to extract structured information
  - [**e.g.**](https://www.funtoo.org/Awk_by_Example,_Part_2)

      ```
      BEGIN {
          FS="\n"
          RS=""
          OFS=", "
          ORS="\n\n"
      }
      { print $1 $2 $3 }
      ```

      This will save the above as awk.awk and `awk -f awk.awk ${file}` to print out concatenated the first three items on each line in a block defined by `FS="\n"`(each field appears on its own line) and `RS=""`(each record is separated by a blank line), demilited by `OFS=", "`, with each line ending with `ORS="\n\n"`.

- combine `grep` and `sort` to search for repeated lines with line number
  - [**e.g.**](https://unix.stackexchange.com/questions/113719/unix-command-to-check-if-any-two-lines-in-a-file-are-same/113761)

      ```
      grep -nFx "$(sort ${file} | uniq -d)" ${file}
      ```

      The inner `$(sort ${file} | uniq -d)` lists each line that occurs more than once. The outer `grep -nFx` looks again `${file}` for exact `-x` matches to any of these lines `-F` and prepends their line number `-n`.

- list non-directory files
  - [**`ls -p | grep -v /`**](https://unix.stackexchange.com/questions/48492/list-only-regular-files-but-not-directories-in-current-directory) (not a backslash!)
  - [**`ls -pL | grep -v /`**](https://unix.stackexchange.com/questions/48492/list-only-regular-files-but-not-directories-in-current-directory) to dereference symbolic links

- About **```shuf (gshuf)```**
  - to shuffle text, ```shuf text_to_shuffle.txt```
  - randomly pick up N lines from a file, [**```gshuf -n N input > output```**](https://stackoverflow.com/questions/9245638/select-random-lines-from-a-file-in-bash)

- About [**```screen```**](https://dev.to/thiht/learn-to-use-screen-a-terminal-multiplexer-gl)
  - ```screen -ls```
  - ```screen -x <session ID>```


======================================================================================

<h2>Terminal Hacking</h2>

```base64```: to encode string, ```base64 <<< string```



======================================================================================


<h2>Markdown</h2>

<h3>useful pages</h3>

- [cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

<h3>tips</h3>

======================================================================================

<h2>Linux</h2>

- shortcut
  - switch between workspaces: `Ctrl+Alt+up/down` or `Super+Page Up/Page Down`
  - re-size the window
    - `Super+up` (full size)
    - `Super+down` (smaller)
    - `Super+left` (left half)
    - `Super+right` (right half)
  - switch between windows: `Super/Alt/Ctrl+tab`
  - switch between input sources: `Super+space`
  - show all windows in a workspace: `Super`

- ?how to add input source such as Chinese/Japanese?

======================================================================================

<h2>Google Sheet</h2>

- [shortcut](https://support.google.com/docs/answer/181110?co=GENIE.Platform%3DDesktop&hl=en)
  - insert row: `Alt+i+r`

======================================================================================

<h2>Atom</h2>

- preview `.md`: `Ctrl+Shift+m`

======================================================================================

<h2>Sublime Text</h2>

======================================================================================

<h2>Good to know (better late than never)</h2>

- Active learning: the learning algorithm can figure out what kind of data they need most and query the users! whoa kewl!
- [set locale](http://www.iac.es/sieinvens/siepedia/pmwiki.php?n=Tutorials.LinuxLocale): ```export LC_CTYPE=zh_CN.UTF-8``` if Chinese does not show up

======================================================================================

<h2>Mamechishiki 豆知識</h2>

- Mebibyte (MiB): 1 MiB = 2<sup>20</sup> bytes = 1024 kibibytes = 1,048,576 bytes

  1 MB = 1,000,000 (10<sup>6</sup>) bytes
