<h2>Python</h2>

- [**tuple/list comparson**](https://docs.python.org/3/reference/expressions.html#value-comparisons): tuples and lists are compared lexicographically.
  - e.g. `(1, 2) < (2, 1) == True` # as the first tuple _comes_ before the second one
  - e.g. `[2, 3] < [1, 8] == False`
  

<h2>Shell (Bash)</h2>

- useful pages: [**use commands and pipes to "mine" and extract data**](http://teaching.idallen.com/cst8207/13w/notes/805_data_mining.html);

- combine `cut`, `awk` and `sed` to slice/extract text, often used in text preprocessing (btw Shell is quite ideal for dealing with text)
  - e.g.
     
     `cut -f ${column_num} ${oldfile} | \`
            
     `sed '/^#/ d' > ${newfile}`
     
     `RS` and `FS` defines the beginning and the end of a block in the `${oldfile}` -- in a corpus, a sentence together wiht its word-level annotation usually constitutes a block; `cut` then extracts the information at the `${column_num}`th column; at the end `sed` `d`eletes all the lines beginning (`^`) with a `#`, and saves the resultant text to `${newfile}`.
- for search, can use `awk`, `sed` or more generally `grep`
  - e.g. `awk '/<something>/' ${file}`  `sed -n '/<something>/p' ${file}` `grep "something" ${file}`
- use `sed` to delete a specific line from a file
  - `sed '1d' ${file}` to remove the first line from the file
