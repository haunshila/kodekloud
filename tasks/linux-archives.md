### Compress an Entire Directory or a Single File
```
tar -czvf name-of-archive.tar.gz /path/to/directory-or-file
```
Here’s what those switches actually mean:

* -c: Create an archive.
* -z: Compress the archive with gzip.
* -v: Display progress in the terminal while creating the archive, also known as “verbose” mode. The v is always optional in these commands, but it’s helpful.
* -f: Allows you to specify the filename of the archive.

#### Compress Multiple Directories or Files at Once
```
tar -czvf archive.tar.gz /home/ubuntu/Downloads /usr/local/stuff /home/ubuntu/Documents/notes.txt

```
