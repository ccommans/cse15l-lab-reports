## Introduction
The command I will be looking at is `find`. Its general use for a recursive file search is:

`$ find [path] [expression]`

where `[path]` is the starting directory and `[expression]` is a set of options that specify the criteria for finding files. This report will examine the following options in the docsearch repository: `-name`, `-type`, `-size`, and `-exec`. ChatGPT was used as a starting point for each of these options' uses, but I also researched them at other sites to ensure ChatGPT's explanation was correct.

## -name option
`-name "str"` allows for a search of filenames that exactly match `"str"` or use a pattern with `*`.

**1. Search for all text files in a directory**
```
$ find ./written_2/non-fiction/OUP/Castro -name "*.txt"
./written_2/non-fiction/OUP/Castro/chR.txt
./written_2/non-fiction/OUP/Castro/chP.txt
./written_2/non-fiction/OUP/Castro/chQ.txt
./written_2/non-fiction/OUP/Castro/chB.txt
./written_2/non-fiction/OUP/Castro/chC.txt
./written_2/non-fiction/OUP/Castro/chA.txt
./written_2/non-fiction/OUP/Castro/chV.txt
./written_2/non-fiction/OUP/Castro/chW.txt
./written_2/non-fiction/OUP/Castro/chM.txt
./written_2/non-fiction/OUP/Castro/chZ.txt
./written_2/non-fiction/OUP/Castro/chL.txt
./written_2/non-fiction/OUP/Castro/chN.txt
./written_2/non-fiction/OUP/Castro/chY.txt
./written_2/non-fiction/OUP/Castro/chO.txt
```
Any text files can now be found only by knowing the directory they are in, which may contain many more files that prohibit a simple search manually. Additionally, this output can be placed in a separate .txt file for database purposes.

**2. Search for a specific word in filename**
```
$ find ./written_2 -name "*Berlin*"                    
./written_2/travel_guides/berlitz2/Berlin-WhereToGo.txt
./written_2/travel_guides/berlitz2/Berlin-History.txt
./written_2/travel_guides/berlitz2/Berlin-WhatToDo.txt
```
This is useful when only one part of the filename is known that may have been lost in many subdirectories.

\[[Source](https://www.plesk.com/blog/various/find-files-in-linux-via-command-line/)]

## -type option
`-type T` searches for files of a given type. Replace `T` in order to search specifically for:
- f: a regular file
- d: directory
- l: symbolic link
- c: character devices
- b: block devices
- p: named pipe (FIFO)
- s: socket

Very few of these are applicable for our simple database, so only the first two will be used.

**1. Search for all files in a directory**
```
$ echo hi > hi.java
$ cp hi.java written_2/non-fiction/OUP/Fletcher 
$ find written_2/non-fiction/OUP/Fletcher -type f
written_2/non-fiction/OUP/Fletcher/ch2.txt
written_2/non-fiction/OUP/Fletcher/hi.java
written_2/non-fiction/OUP/Fletcher/ch1.txt
written_2/non-fiction/OUP/Fletcher/ch5.txt
written_2/non-fiction/OUP/Fletcher/ch6.txt
written_2/non-fiction/OUP/Fletcher/ch9.txt
written_2/non-fiction/OUP/Fletcher/ch10.txt
```
As shown, all files appear and can give a better idea of the file's contents without having to use `-name` for each type of file.

**2. Search for all directories**
```
$ find written_2 -type d
written_2
written_2/non-fiction
written_2/non-fiction/OUP
written_2/non-fiction/OUP/Berk
written_2/non-fiction/OUP/Abernathy
written_2/non-fiction/OUP/Rybczynski
written_2/non-fiction/OUP/Kauffman
written_2/non-fiction/OUP/Fletcher
written_2/non-fiction/OUP/Castro
written_2/travel_guides
written_2/travel_guides/berlitz1
written_2/travel_guides/berlitz2
```
This gives a good idea of what the database structure looks like without having to scroll past each directory's contents if simply `find written_2` was called.

\[[Source](https://linuxize.com/post/how-to-find-files-in-linux-using-the-command-line/)]

## -size option
`size +/- n S` will search for a file of a given size. `S` is the unit of file size being searched for, `n` is how many of `S` will be searched for, `+` will look for files with size greater than `n S` and `-` will look for files with size less than `n S`. Replace `S` to search in:
- b: 512-byte blocks (default)
- c: bytes
- w: two-byte words
- k: Kilobytes
- M: Megabytes
- G: Gigabytes

Since text files are small, we will use Kilobytes to demonstrate.

**1. Search for > 100 kB text files**
```
$ find written_2 -size +100k                            
written_2/non-fiction/OUP/Berk/ch2.txt
written_2/non-fiction/OUP/Berk/CH4.txt
written_2/travel_guides/berlitz1/WhereToIndia.txt
written_2/travel_guides/berlitz1/WhereToItaly.txt
written_2/travel_guides/berlitz1/WhereToMalaysia.txt
written_2/travel_guides/berlitz1/WhereToJapan.txt
written_2/travel_guides/berlitz1/WhereToFrance.txt
written_2/travel_guides/berlitz2/Portugal-WhereToGo.txt
written_2/travel_guides/berlitz2/Canada-WhereToGo.txt
written_2/travel_guides/berlitz2/China-WhereToGo.txt
```
Searching for large files is especially useful when needing to free up storage somewhere, and the freedom so search for any size can help quickly find the largest file to remove.

**2. Search for < 5 kB text files**
```
$ find written_2 -type f -size -5k
written_2/travel_guides/berlitz1/HandRLasVegas.txt
written_2/travel_guides/berlitz1/HandRIstanbul.txt
written_2/travel_guides/berlitz1/HandRHongKong.txt
written_2/travel_guides/berlitz1/WhatToHawaii.txt
written_2/travel_guides/berlitz1/HandRLisbon.txt
written_2/travel_guides/berlitz1/HandRMallorca.txt
written_2/travel_guides/berlitz1/WhatToFrance.txt
written_2/travel_guides/berlitz1/HandRLosAngeles.txt
written_2/travel_guides/berlitz1/HandRMadeira.txt
written_2/travel_guides/berlitz1/HandRIbiza.txt
written_2/travel_guides/berlitz1/HandRLakeDistrict.txt
written_2/travel_guides/berlitz1/WhereToHawaii.txt
written_2/travel_guides/berlitz1/HandRJerusalem.txt
```
Without the `-type f`, directories would have also been included in the output. Small files may not take up much storage, but they also could be unnecessary garbage files (e.g. outputs when testing a program that writes files) that can be removed to clean up a directory.

\[[Source1](https://linuxconfig.org/how-to-use-find-command-to-search-for-files-based-on-file-size)]

\[[Source2](https://linuxnightly.com/find-files-based-on-size-in-linux/)]

## -exec option
`-exec [cmd] {} \;` will execute `[cmd]` on the all paths returned by `find`.

**1. Use grep/search for a specific word in text files**
```
$ find written_2 -name "*.txt" -exec grep -l "Lucayans" {} \;
written_2/travel_guides/berlitz2/Bahamas-History.txt
```
`grep` is now being used on every text file in the database instead of individually searching through the text files with `grep`.

> NOTE: this is slightly different than `grep -r`, since `find` above restricts the search to text files, whereas `grep -r` may look through other types of files (.java, .sh, etc.).

**2. Use rm/remove on all small files**
```
find written_2 -type f -size -5k -exec rm -i {} \;
remove written_2/travel_guides/berlitz1/HandRLasVegas.txt? n
remove written_2/travel_guides/berlitz1/HandRIstanbul.txt? n
remove written_2/travel_guides/berlitz1/HandRHongKong.txt? n
remove written_2/travel_guides/berlitz1/WhatToHawaii.txt? n
remove written_2/travel_guides/berlitz1/HandRLisbon.txt? n
remove written_2/travel_guides/berlitz1/HandRMallorca.txt? n
remove written_2/travel_guides/berlitz1/WhatToFrance.txt? n
remove written_2/travel_guides/berlitz1/HandRLosAngeles.txt? n
remove written_2/travel_guides/berlitz1/HandRMadeira.txt? n
remove written_2/travel_guides/berlitz1/HandRIbiza.txt? n
remove written_2/travel_guides/berlitz1/HandRLakeDistrict.txt? n
remove written_2/travel_guides/berlitz1/WhereToHawaii.txt? n
remove written_2/travel_guides/berlitz1/HandRJerusalem.txt? n
```
This essentially does automatically (if `-i` is removed) the benefit of using `-size` without having to afterward go into the directory and remove each file individually.

\[[Source](https://www.baeldung.com/linux/find-exec-command)]
