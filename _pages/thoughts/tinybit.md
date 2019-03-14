<h2>Regex</h2>

- Chinese `\u4E00-\u9FA5`

======================================================================================

<h2>Python</h2>

<h3>useful pages</h3>

- [FlashText: alternative of regexp](https://medium.freecodecamp.org/regex-was-taking-5-days-flashtext-does-it-in-15-minutes-55f04411025f)

<h3>useful packages</h3>

- `tqdm` for progress bar
- [pyahocorasick](https://pypi.org/project/pyahocorasick/) for efficient string matching

<h3>tips</h3>

- set instance pointer
	- `a = b = set()` a and b point to the same object! so they change with each other

- `random.shuffle(list())` in-place, so shouldn't print the NoneType object, instead, should print the original list

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

- print to stdout or file if file specified
  - ```print(out, file=fout)```

- `sort()` does sorting in place; while `.sorted()` returns a new array as sorted

- `os.system()` to run subshell

- don't overuse `write()`

- `du -h -d1` & `du -sh`: check storage

- use `set()` more to save time!

======================================================================================

<h2>Conda</h2>

- [`conda install notebook ipykernel`](https://stackoverflow.com/questions/30492623/using-both-python-2-x-and-python-3-x-in-ipython-notebook/37857536#comment94230432_37857536)

======================================================================================

<h2>Shell (Bash)</h2>

<h3>Stupid frequent errors</h3>
- when running a shell script which includes routes/paths direction, must check them carefully! (especially when there is route/path redirection!
- if stuck, check line by line! instead of running the whole script

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

- `file <file>` check file type else empty

- `awk -F "\t" '{if ($4=="something"){print $0}}' out.anonymous.all.txt | wc -l`: (count lines that have something at the 4th column) use `awk` to catch lines that meet the condition

- combine `cut`, `awk` and `sed` to slice/extract text, often used in text preprocessing (btw Shell is quite ideal for dealing with text)
  - e.g.

      ```
      cut -f ${column_num} ${oldfile} | \
      sed '/^#/ d' > ${newfile}
      ```

     `cut` then extracts the information at the `${column_num}`th column; at the end `sed` `d`eletes all the lines beginning (`^`) with a `#`, and saves the resultant text to `${newfile}`.
     
- using `awk` to deal with blocks of data: `awk 'BEGIN{b=0} { if ($1!="========") {printf ("%d\t%s\n", b, $1);} else {b+=1}}' slotsbycluster | sort | uniq -c | sort -k2,2n -k1,1nr`
     
- cut using comma as the delimiter
  - e.g.
  
      ```cut -d<delimiter> -f<col> <file>```

- keep unique items only
  - e.g.
  
      ```sort | uniq```

- replace with tab
  - e.g.
  
      ```tr ',' '\t' < <in.file> > <out.file>```
      
- remove trailing tabs: `sed 's/[[:blank:]]*$// <file>`

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

- permutation
  - ```echo {a,b}{1,2}``` will return ```a1 a2 b1 b2```

- back to the previous path
  - `cd -`

- check gpu: `watch -n 1 nvidia-smi`

- check gpu by PID and kill the process: `ps -ef | grep <PID>`; `kill -9 <PID>`


======================================================================================

<h2>Java</h2>

- `mvn clean package install`

- to skip UTs, `mvn clean install -DskipTests`

- `ef bb bf`: BOM(byte-order mark)

- use interface names as input arguments but the exact class names as return type: `public static ArrayList<String> func(List<Integer>) {}` can avoid being hard-coded

- `final`: variabes declared as final can only be assigned once

- Data types:
	* `List<String> l = Arrays.asList("a", "b")`: create a fixed-length array whose elements cannot be added/removed but could be modified like this: `l.set(0, "c")`; however, if created like this: `List<String> l = new Array<String>(Arrays.asList("a", "b"))`, the arraylist could be added/removed of elements



======================================================================================

<h2>C/C++</h2>

- Do not simply copy complied files to somewhere else. Instead, should `make clean` and compile it again


======================================================================================

<h2>Terminal Hacking</h2>

- `base64`: to encode string, ```base64 <<< string```

- `Ctrl+C`: to clear the jobs

- `fg`: to check the left jobs

- `htop`: a better looking `top`

- `hexdump`: a hexadecimal view of computer data; usually as part of debugging



======================================================================================

<h2>Git</h2>

- add submodule: `git submodule add <url> <dir>`
- rebase: checkout to the commit(ID) you want to rebase `git rebase master`
- `git checkout -b`
- `git checkout -B`

======================================================================================

<h2>Docker</h2>

- list docker images: `sudo docker images`
- enter a docker image: `sudo docker run -i -t <image ID>`
- display all docker container IDs: `docker ps -a`; active ones only: `docker ps`
- copy files from a server to a docker container: `docker cp <file-or-dir> <containerID>:<path>` (while writing path, instead of `~/`, use `/root/`
- enter a container: `docker exec -it <mycontainer> /bin/bash`
- restart a dead/inactive container: `docker start <mycontainer>`


<h2>SSH</h2>

- ```ssh-add```: add ssh keys to keychain

======================================================================================

<h2>Json</h2>

- format json string: `bejson.com`

<h2>Markdown</h2>

<h3>useful pages</h3>

- [cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

<h3>tips</h3>

======================================================================================

<h2>UML</h2>

======================================================================================


<h2>XML</h2>

- parse an XML file

	```
	from xml.etree import ElementTree as ET
	xml = '/Users/shijieyao/Library/Containers/com.taobao.Aliwangwang/Data/Library/Application Support/AliWangwang/80profiles/DefaultEmotions/EmotionConfig.xml'
	tree = ET.parse(xml)  
	root = tree.getroot()
	
	for elem in root:
	    print(elem[0].text)
	```

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

<h2>Excel</h2>

- the first line(s) can be frozened

======================================================================================


<h2>Google Sheet</h2>

- [shortcut](https://support.google.com/docs/answer/181110?co=GENIE.Platform%3DDesktop&hl=en)
  - insert row: `Alt+i+r`

======================================================================================

<h2>Jupyter Notebook</h2>

- measure the cell execution time: ```%%time```
- `jupyter notebook --ip 0.0.0.0`

======================================================================================

<h2>Atom</h2>

- preview `.md`: `Ctrl+Shift+m`

======================================================================================

<h2>Sublime Text</h2>

======================================================================================

<h2>Good to know (better late than never)</h2>

- Active learning: the learning algorithm can figure out what kind of data they need most and query the users! whoa kewl!
- [set locale](http://www.iac.es/sieinvens/siepedia/pmwiki.php?n=Tutorials.LinuxLocale): ```export LC_CTYPE=zh_CN.UTF-8``` if Chinese does not show up; for permanent change, write to ~/.bashrc
- always add a newline `\n` to the end of a file

======================================================================================

<h2>Mamechishiki 豆知識</h2>

- Mebibyte (MiB): 1 MiB = 2<sup>20</sup> bytes = 1024 kibibytes = 1,048,576 bytes

  1 MB = 1,000,000 (10<sup>6</sup>) bytes
