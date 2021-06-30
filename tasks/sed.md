### Linux String Substitute (sed)

a. Delete all lines containing word software and save results in /home/BSD_DELETE.txt file. (Please be aware of case sensitivity)
```
# ssh into app server and loggin as root 
sudo -i
# delete all lines starting and ending with spaces and store it into /home/BSD_DELETE.txt
sed '/\<software\>/d' /home/BSD.txt > /home/BSD_DELETE.txt
```
b. Replace all occurrence of word and to is and save results in /home/BSD_REPLACE.txt file
Note: Let's say you are asked to replace word to with from. In that case, make sure not to alter any words containing this string; for example upto, contributor etc.

```
sed 's/\band\b/is/g' /home/BSD.txt > /home/BSD_REPLACE.txt
```
