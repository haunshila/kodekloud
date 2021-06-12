
## Copy Specific File Types While Keeping Directory Structure In Linux
Picture this scenario.

I have a directory named "Linux" with different type of files saved in different sub-directories. Have a look at the following directory structure:
```
$ tree Linux/
Linux/
├── dir1
│   ├── English
│   │   └── Kina - Can We Kiss Forever.mp3
│   ├── Instrumental
│   │   └── Chill Study Beats.mp3
│   └── Tamil
│       ├── Kannan Vanthu.mp3
│       └── yarenna.mp3
├── dir2
│   ├── file.docx
│   └── Raja Raja Chozan Naan.mp3
├── dir3
│   ├── Bamboo Flute - Meditation - Healing - Sleep - Zen.mp3
│   └── pic.jpg
└── dir4
    ├── Aaruyirae.mp3
    └── video.mp4

7 directories, 10 files
```
As you see in the above directory structure, the Linux directory has four sub-directories namely dir1, dir2, dir3 and dir4. The mp3 files are scattered across all four sub-directories. Now, I want to copy all mp3 files to another directory named "ostechnix" and also I want to keep the same directory structure in the target directory.

First we will see how to do this using "find" command.

#### Method 1 - using "find" and "cp" or "cpio" commands
Go to the source directory:

```
$ cd Linux/
```
And copy all mp3 fie types using "find" command:
```
$ find . -name '*.mp3' -exec cp --parents \{\} ~/ostechnix \;
```
Let us break down the above command and see what each option does.

* find – command to find files and folders in Unix-like systems.
* the dot (.) - represents we copy the contents from current directory.
* -name ‘*.mp3’ – search for files matching with extension .mp3.
* -exec cp – execute the ‘cp’ command to copy files from source to destination directory.
* --parents - create the intermediate parent directories if needed to preserve the parent directory structure.
* \{\} – is automatically replaced with the file name of the files found by ‘find’ command. And the braces are escaped to protect them from expansion by the shell in some "find" command versions. You can also use {} without escape characters.
* ~/ostechnix – target directory to save the matching files.
* \; – indicates it that the commands to be executed are now complete, and to carry out the command again on the next match.

This command will find and copy all mp3 type files from ~/Linux directory to ~/ostechnix directory. And also it preserves the same directory structure in the target directory.

You can verify it using "tree" command at both locations like below.

![output-image](https://github.com/haunshila/kodekloud/blob/master/LinuxFind.png)

As you see in the above output, the destination directory only has the mp3 files and its directory structure is same as source directory.

If you are doing this from some other location, specify the full path of source directory like below.
```
$ find ~/Linux -name '*.mp3' -exec cp --parents \{\} ~/ostechnix \;
```

This command will find all of the file in Linux/<sub-directories> location and copy them to ostechnix/~/Linux/<sub-directories>.

If --parents option doesn't work, you can combine find command with cpio command to copy files keeping directory structure.
```
$ find . -name '*.mp3' | cpio -pdm  ~/ostechnix
```

Here,

* cpio - Command to copy files to and from archives.
* -p - Read a list of file names from the standard input and copy them to the specified directory.
* -d - Create directories where needed.
* -m - Preserve file modification time.

For more details, refer man pages.
```
$ man find
$ man cp
$ man cpio
```

#### Method 2 - using Rsync

**Rsync** is a powerful tool used to/from local and remote systems. To copy certain type of files from one directory to another while keeping the parent directory structure, run:
```
$ rsync -a -m --include '*/' --include '*.mp3' --exclude '*' ~/Linux/ ~/ostechnix
-----OR------
$ rsync -a --prune-empty-dirs --include '*/' --include '*.mp3' --exclude '*' ~/Linux/ ~/ostechnix
```
Here,

* rsync - remote (and local) file-copying tool.
* -a - archive mode to preserve almost everything (including symlinks, modification dates, file permissions, owners etc.)
* -m, --prune-empty-dirs - prune empty directories from source tree. If you want to include empty directories, just remove this option from the above command.
* --include="*/" --include="*.mp3" --exclude="*" - To include only specific files, you first need to include those specific files, then exclude all other files. In our case, we have included *.mp3 files and exclude everything else.
* ~/Linux - Source directory.
* ~/ostechnix - Destination directory.

For more details, refer man pages.
```
$ man rsync
```
