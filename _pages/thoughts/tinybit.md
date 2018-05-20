<h2>Python</h2>

<h3>useful pages</h3>

- <...>

<h3>tips</h3>

- [**tuple/list comparson**](https://docs.python.org/3/reference/expressions.html#value-comparisons): tuples and lists are compared lexicographically.
  - e.g. `(1, 2) < (2, 1) == True` # as the first tuple _comes_ before the second one
  - e.g. `[2, 3] < [1, 8] == False`

======================================================================================

<h2>Shell (Bash)</h2>

<h3>useful pages</h3>

- [**use commands and pipes to "mine" and extract data**](http://teaching.idallen.com/cst8207/13w/notes/805_data_mining.html);

<h3>tips</h3>

- frequent errors (that I usually make!):
  - extra `|` before `<`, especially at the last line before `<`

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
      
      ```grep "something" ${file}```
      
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
      
- 
