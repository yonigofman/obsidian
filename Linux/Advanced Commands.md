
| Command | Description                            |
| ------- | -------------------------------------- |
| `awk`   | Text processing and pattern scanning   |
| `grep`  | Searching for patterns in files        |
| `sed`   | Stream editor for text transformations |
| `sort`  | Sorting lines of text files            |
| `cut`   | Extracting sections from lines         |
| `tr`    | Translating or deleting characters     |

### `awk`

| Flag         | Description                            | Example                                      |
| ------------ | -------------------------------------- | -------------------------------------------- |
| `-F`         | Specifies field separator              | `awk -F',' '{print $2}' file.csv`            |
| `-v`         | Assigns a variable                     | `awk -v var="value" '{print var}'`           |
| `NR`         | Number of records (lines) processed    | `awk 'NR > 1 {print}' file.txt`              |
| `NF`         | Number of fields in the current record | `awk 'NF > 3 {print}' file.txt`              |
| `/pattern/`  | Pattern to match                       | `awk '/error/ {print $0}' file.log`          |
| `{ action }` | Action to perform                      | `awk '{sum += $1} END {print sum}' file.txt` |
|              |                                        |                                              |

### `grep`

|Flag|Description|Example|
|---|---|---|
|`-i`|Performs case-insensitive search|`grep -i 'pattern' file.txt`|
|`-v`|Inverts the match (prints lines not matching)|`grep -v 'pattern' file.txt`|
|`-r`|Recursively search directories|`grep -r 'pattern' /path/to/directory`|
|`-n`|Prints line numbers with matching lines|`grep -n 'pattern' file.txt`|
|`-o`|Prints only the matched part of the line|`grep -o 'pattern' file.txt`|
|`-E`|Uses extended regular expressions|`grep -E 'pattern1|

### More Advanced Commands:

#### `sed`

|Flag|Description|Example|
|---|---|---|
|`-e`|Adds a script to be executed|`sed -e 's/old/new/g' file.txt`|
|`-n`|Suppresses automatic printing of pattern space|`sed -n '/pattern/p' file.txt`|
|`-i`|Edits files in place|`sed -i 's/old/new/g' file.txt`|
|`-r`|Uses extended regular expressions|`sed -r 's/pattern/new/g' file.txt`|
|`s/old/new/`|Substitutes "old" with "new"|`sed 's/old/new/g' file.txt`|

#### `sort`

|Flag|Description|Example|
|---|---|---|
|`-r`|Reverses the result of comparisons|`sort -r file.txt`|
|`-n`|Compares according to string numerical value|`sort -n file.txt`|
|`-k`|Sorts by a specific key|`sort -k 2,2 file.txt`|
|`-t`|Specifies field separator|`sort -t',' -k2 file.csv`|
|`-u`|Removes duplicate lines|`sort -u file.txt`|

#### `cut`

|Flag|Description|Example|
|---|---|---|
|`-d`|Specifies field delimiter|`cut -d',' -f1,3 file.csv`|
|`-f`|Selects only these fields|`cut -f1,3 file.txt`|
|`--complement`|Prints the complement of selected bytes|`cut --complement -d',' -f1 file.csv`|
|`--output-delimiter`|Specifies output delimiter|`cut --output-delimiter='-' -d' ' -f1,3 file.txt`|
|`--characters`|Selects only these characters|`cut --characters=1-5,10-15 file.txt`|

#### `tr`

|Flag|Description|Example|
|---|---|---|
|`-d`|Deletes characters specified in set1|`tr -d '[:digit:]' < file.txt`|
|`-s`|Squeezes repeated characters|`tr -s ' ' < file.txt`|
|`[:class:]`|Represents a character class|`tr '[:lower:]' '[:upper:]' < file.txt`|
|`-c`|Complements set of characters|`tr -c '[:digit:]' '*' < file.txt`|
|`--delete`|Deletes characters in set1|`tr --delete '[:space:]' < file.txt`|
