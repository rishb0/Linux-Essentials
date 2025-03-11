### **STRING PROCESSING IN LINUX**

**Why is string processing used?**
String processing is commonly used to filter and extract specific parts of output from commands such as `ifconfig`, `ip a`, etc.


# `Head`
The `head` command is used to display the first few lines of a file. By default, it shows the first 10 lines.

### Syntax
```bash
head [options] [file]
```

### Examples:-
Display the first 10 lines of a file:
```bash
head filename.txt
```

Display the first 5 lines:
```bash
head -n 5 filename.txt
```

Display the first 20 lines:
```bash
head -n 20 filename.txt
```

# `Tail`
The `tail` command is used to display the last few lines of a file. By default, it shows the last 10 lines.

### Syntax
```bash
tail [options] [file]
```

### Examples:-
Display the last 10 lines of a file:
```bash
tail filename.txt
```

Display the last 5 lines:
```bash
tail -n 5 filename.txt
```

Continuously monitor a file for new lines (useful for logs):
```bash
tail -f /var/log/syslog
```


# `wc`
The `wc` (word count) command counts the number of lines, words, and characters in a file.

### Syntax
```bash
wc [options] [file]
```

### Examples:-
Count lines, words, and characters:
```bash
wc filename.txt
```

Count only lines:
```bash
wc -l filename.txt
```

Count only words:
```bash
wc -w filename.txt
```

Count only characters:
```bash
wc -c filename.txt
```


# `sort`
The `sort` command is used to arrange lines in text files in a particular order.

### Syntax
```bash
sort [options] [file]
```

### Examples:-
Sort a file alphabetically:
```bash
sort filename.txt
```

Sort in reverse order:
```bash
sort -r filename.txt
```

Sort a file numerically:
```bash
sort -n numbers.txt
```

Sort a file and remove duplicates:
```bash
sort -u filename.txt
```


# `watch`
The `watch` command is used to execute a program periodically and show the output in real-time.

### Syntax
```bash
watch [options] command
```

### Examples:-
Monitor file changes every 2 seconds:
```bash
watch -n 2 ls -l
```

Monitor memory usage:
```bash
watch free -m
```

Monitor disk usage changes:
```bash
watch df -h
```


# `grep`
The `grep` command searches for a pattern in a file and prints matching lines.

### Syntax
```bash
grep [options] pattern [file]
```

### Examples:-
Find occurrences of 'searchword' in a file:
```bash
grep searchword filename
```

Find 'root' in the `/etc/passwd` file:
```bash
grep "root" /etc/passwd
```

Find 'root' in multiple files:
```bash
grep root /etc/passwd /etc/shadow
```

Perform case-insensitive search:
```bash
grep -i root messages
```

Find multiple words ('session', 'root', or 'mounting'):
```bash
grep -E "(session|root|mounting)" var/log/messages
```

Find lines containing both 'session' and 'root':
```bash
grep "session" var/log/messages | grep root
```

Find lines with 'session' but not 'root':
```bash
grep "session" var/log/messages | grep -v root
```

Find lines where 'root' appears at the start:
```bash
grep "^root" var/log/messages
```

Find lines where 'root' appears at the end:
```bash
grep "root.$" var/log/messages
```

Find logs for 'root' on 2nd September:
```bash
grep "^2sep" var/log/messages | grep root
```

Find 'roo' followed by any single character:
```bash
grep 'roo.' filename
```

Find 'roo' followed by two characters:
```bash
grep 'roo..' filename
```

Find empty lines in a file:
```bash
grep '^$' filename
```

Exclude lines starting with `#`:
```bash
grep -v '^#' ssd_config
```

Find all alphanumeric characters:
```bash
grep "[[:alnum:]]" filename
```

Search for domains from `domain.txt` in `url.txt`:
```bash
grep -f domain.txt url.txt
```
# `cut`
The `cut` command extracts sections of each line from a file or standard input.

### Syntax
```bash
cut [options] [file]
```

### Examples:-
Extract the first 10 characters from each line:
```bash
cut -c 1-10 filename.txt
```

Extract only the second column from a CSV file:
```bash
cut -d',' -f2 data.csv
```

Extract multiple fields (1st and 3rd columns):
```bash
cut -d',' -f1,3 data.csv
```

Extract usernames from the `/etc/passwd` file:
```bash
cut -d':' -f1 /etc/passwd
```


# `paste`
The `paste` command merges lines from multiple files, joining them side by side.

### Syntax
```bash
paste [options] [file]
```

### Examples:-
Merge two files line by line:
```bash
paste file1.txt file2.txt
```

Merge using a custom delimiter (comma):
```bash
paste -d ',' file1.txt file2.txt
```

Merge three files side by side:
```bash
paste file1.txt file2.txt file3.txt
```

Merge without spaces between columns:
```bash
paste -d '' file1.txt file2.txt
```

Combine columns from `/etc/passwd`:
```bash
cut -d':' -f1 /etc/passwd | paste -d ',' - file.txt
```

# `awk`
The `awk` command processes text based on patterns and actions.

### Syntax
```bash
awk 'pattern {action}' filename
```

### Examples:-
Print all lines of a file:
```bash
awk '{print $0}' filename
```

Print the first field (column) using `:` as the delimiter:
```bash
awk -F: '{print $1}' filename
```

Print the first, second, and third fields:
```bash
awk -F: '{print $1, $2, $3}' filename
```

Extract the second field from `ifconfig` output:
```bash
ifconfig | awk '{print $2}'
```

Find and print only `inet` addresses:
```bash
ifconfig | awk '/inet /{print $2}'
```

Print a custom message before and after execution:
```bash
ifconfig | awk 'BEGIN{print "== IP Address =="} /inet /{print $2} END{print "====="}'
```

Process input text with BEGIN and END blocks:
```bash
echo "one two three four" | awk 'BEGIN {print "=== Start ==="} {print $0} END {print "-- Stop --"}'
```

Print specific fields with separators:
```bash
echo "one two three four" | awk 'BEGIN {print "=== start ==="} {print $1, " - ", $2} END {print "-- stop --"}'
```

Use different separators:
```bash
echo "one two three four" | awk 'BEGIN {print "=== start ==="} {print $1, " / ", $2} END {print "-- stop --"}'
```

Print fields with newline formatting:
```bash
echo "one two three four" | awk 'BEGIN {print "=== start ==="} {print $1, "\n", $2} END {print "-- stop --"}'
```

Modify text dynamically:
```bash
echo "armour infosec" | awk '{$1="ARMOUR"; print $1}'
```

Filter and print lines from `/etc/passwd`:
```bash
cat /etc/passwd | awk -F: '$1=="root" {print $0}'
```

Exclude specific lines:
```bash
cat /etc/passwd | awk -F: '$1!="root" {print $0}'
```

Print lines where the third field is zero:
```bash
cat /etc/passwd | awk -F: '$3==0 {print $0}'
```

Print lines where the third field is greater than 1000:
```bash
cat /etc/passwd | awk -F: '$3>=1000 {print $0}'
```

Find Ethernet addresses:
```bash
ifconfig | awk '$1=="ether" {print $2}'
```

Print the number of fields in a line:
```bash
echo "one two three four" | awk '{print NF}'
```

Print the last field of a line:
```bash
echo "one two three four" | awk '{print $NF}'
```

Print the second-to-last field:
```bash
echo "one two three four" | awk '{print $(NF-1)}'
```

Print the last and second-to-last fields:
```bash
echo "one two three four" | awk '{print $NF, $(NF-1)}'
```

Process `/etc/passwd` and extract fields:
```bash
cat /etc/passwd | awk '{print NF}'
cat /etc/passwd | awk '{print $NF}'
cat /etc/passwd | awk '{print $NF, $(NF-1)}'
```

# `sed`
The `sed` command performs text manipulation and pattern matching operations.

### Syntax
```bash
sed [options] 'command' filename
```

### Examples:-

#### Basic Commands:
Append text after a line:
```bash
sed '/pattern/a text' filename.txt
```

Delete a specific pattern:
```bash
sed '/pattern/d' filename.txt
```

Insert text before a line:
```bash
sed '/pattern/i text' filename.txt
```

Print lines that match a pattern:
```bash
sed -n '/pattern/p' filename.txt
```

Quit `sed` processing early:
```bash
sed '/pattern/q' filename.txt
```

#### Substitution Operations:
Replace a word:
```bash
sed 's/oldword/newword/' filename.txt
```

Replace all occurrences of a word:
```bash
sed 's/oldword/newword/g' filename.txt
```

Replace the first occurrence only:
```bash
sed 's/oldword/newword/1' filename.txt
```

Replace the second occurrence only:
```bash
sed 's/oldword/newword/2' filename.txt
```

Replace text using extended regex:
```bash
sed -r 's/[0-9]+/***/g' filename.txt
```

#### Line-Based Operations:
Print the first and second lines:
```bash
sed -n '1,2p' /etc/passwd
```

Print only empty lines:
```bash
sed -n '/^$/p' /etc/passwd
```

Print all non-empty lines:
```bash
sed -n '/^$/!p' /etc/passwd
```

Print the last line:
```bash
sed -n '$p' /etc/passwd
```

Delete lines from the 5th to the last:
```bash
sed '5,$d' /etc/passwd
```

#### Advanced Usage:
Replace all `/` occurrences:
```bash
sed 's#/#-#g' filename.txt
```

Convert uppercase to lowercase in a pattern:
```bash
sed 's/\([A-Z]\)/(\1)/g' filename.txt
```

Print lines containing `root` and the next 3 lines:
```bash
sed -n '/root/,+3p' /etc/passwd
```

Delete all lines containing digits:
```bash
sed '/[[:digit:]]/d' filename.txt
```

Change text where `arnold` appears:
```bash
sed '/arnold/c ARNOLD User' filename.txt
```

Quit processing when `arnold` is found:
```bash
sed '/arnold/q' filename.txt
```

Execute shell commands inside `sed`:
```bash
sed '1e date' filename.txt
```

Replace numbers with asterisks:
```bash
echo "User ID 1000" | sed 's/[0-9]\+/*****/'
```

#### Multiple `sed` commands:
Print lines containing `arnold` and `root`:
```bash
sed -ne '/arnold/p' -ne '/root/p' filename.txt
```

Append and insert text around a pattern:
```bash
sed -e '/arnold/a "+++++++++++++++++++++"' -e '/arnold/i "---------------------"' filename.txt
```

Modify files in place:
```bash
sed -i -e '/arnold/a "+++++++++++++++++++++"' -e '/arnold/i "---------------------"' filename.txt
```