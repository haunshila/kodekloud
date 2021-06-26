### Linux String Substitute

* Find and Replace the First Occurrence
```
$ sed -i 's/{OLD_TERM}/{NEW_TERM}' {file}
# Now let’s apply this command to our example: replace first occurence of About into Cloud
$ sed -i 's/About/Cloud/' /root/test.txt

```
* Find and Replace All Occurrences
```
$ sed -i 's/{OLD_TERM}/{NEW_TERM}/g' {file}
# Let’s apply this command to our example: replace all occurence of About into Cloud
$ sed -i 's/About/Cloud/g' /root/test.txt

```


Ref:-
https://www.baeldung.com/linux/find-replace-text-in-file
