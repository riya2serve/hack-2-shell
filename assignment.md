# Question 1: Get the data files 

Download the following data files from the internet using the ```curl``` command: 'http://eaton-lab.org/pdsb/test.fastq.gz'and 'http://eaton-lab.org/pdsb/iris-data-dirty.csv.' Use the ```less``` or ```zless``` commands to look at each file. Describe what these commands do. Finally, use the ```head``` command to print the first 5 lines of the file 'iris-data-dirty.csv'.

I first refreshed myself on the curl command and basic syntax for it. The ```curl``` command allows users to fetch a given URL or file from the bash shell. I used a 301-redirect file with curl to download the .fastq.gz file into a new, empty file that I named 'file.tgz.' I repeated this for the .csv file, downloading it into a new file named 'file.csv'. I then used the ```less``` command, to view both files page-by-page. This command makes it possible to view the contents of files without downloading them into the operating system's memory. As a result, I was able to speed up the file loading process for both 'file.tgz' and 'file.csv'. The ```zless``` command (not used) is slightly different in that it paginates the output. The last thing I did was to use the ```head``` command to print the first 5 lines of the iris-data-dirty.csv file. By default this command prints the first 10 lines, so to account for this, I had to ammend the command by adding the ```-n num``` argument 
```
curl -L -o file.tgz http://eaton-lab.org/pdsb/test.fastq.gz
less file.tgz
```
```
 % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   162  100   162    0     0    552      0 --:--:-- --:--:-- --:--:--   552
100  220k  100  220k    0     0   473k      0 --:--:-- --:--:-- --:--:--  473k
```
```
file.tgz may be a binary file. See it anyway?
```
```
Yes
```
```
(previous)...
Ҭ<94>`Y<E9>\<B8><DD> <A9><B9><CB>^Mѕ/<E6><DB>^Brrf<89><U+0082><99>^Z<8F>N~c<E0>ޮtc2<96>IE<A0><F1>PA!<D3>H<FD>^\^Ye^P<A2>a^GP<AC>P@^As<8D>'^A^]<96>y<B2>\XS<BC><9<98><D4>^^      ^_<8B><84>YA<9D><CB>^Q<AC><99><C5><E5><88>h ^F<F0><C5>[<8A>^NX<C<C6><CF>$<85><DF><F6><87><EA>r<FB>><DB><FF>?<EC><D7>^^c<FA><C1>^M^@
```

```
curl -L -o file.csv http://eaton-lab.org/pdsb/iris-data-dirty.csv
less file.csv
```
```
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   162  100   162    0     0    964      0 --:--:-- --:--:-- --:--:--   970
100  4549  100  4549    0     0  17117      0 --:--:-- --:--:-- --:--:-- 17117
```
```
(previous)...
6.1,2.6,5.6,1.4,Iris-virginica
7.7,3.0,6.1,2.3,Iris-virginica
6.3,3.4,5.6,2.4,Iris-virginica
6.4,3.1,5.5,1.8,Iris-virginica
... (continued)
```
```
head -n 5 file.csv
```
```
5.1,3.5,1.4,0.2,Iris-setosa
4.9,3.0,1.4,0.2,Iris-setosa
4.7,3.2,1.3,0.2,Iris-setosa
4.6,3.1,1.5,0.2,Iris-setosa
5.0,3.6,1.4,0.2,Iris-setosa
```
# Question 2: Clean the data 

Use ```grep```, ```uniq```, and ```sed``` for this question. Check that all of the species names are spelled correctly in the file 'iris-data-dirty.csv'. Also check for missing values stored as NA. Create a new file where mispelled names are replaced with the correct values, and lines with "NA" are excluded, and save it as 'iris-data-clean.csv'. Use ```cut```, ```sort``` and ```uniq``` to list the number of data values there are for each species in the new cleaned data file. Describe your work.

The ```head``` command revealed species names within the file 'iris-data-dirty.csv' are located in the 5th column. To inspect the species name for any misspellings I used the ```cut``` command and piped it into the ```sort```and ```uniq``` commands. This allowed me to extract the species name column, sort them, and then display unique (i.e. misspelled) values. To check for missing values in the .csv file I used the ```grep``` command, which searches for user-selected expressions (e.g. NA) that you want it to search a file for. After accomplishing this, I created a new clean file. I first used the ```sed``` command to replace misspelled species names. I also removed missing values using ```grep -v```, which excludes lines with NA. This new file was saved as 'iris-data-clean.csv'. My last step was to count the number of data points for each species using the ```cut```, ```sort```, and ```uniq``` commands. 

```
cut -d ',' -f 5 file.csv | sort | uniq
```
```       
Iris-setosa
Iris-setsa
Iris-versicolor
Iris-versicolour
Iris-virginica
```
```
grep 'NA' file.csv
```
```
6.3,NA,4.9,1.5,Iris-versicolor
5.6,NA,4.1,1.3,Iris-versicolor
```
```
sed 's/[Ss]etsa/setosa/g; s/[Vv]ersicolou*r/versicolor/g' file.csv | grep -v 'NA' > file.clean.csv
```
```
less file.clean.csv
(previous)...
6.9,3.1,5.1,2.3,Iris-virginica
5.8,2.7,5.1,1.9,Iris-virginica
6.8,3.2,5.9,2.3,Iris-virginica
6.7,3.3,5.7,2.5,Iris-virginica
6.7,3.0,5.2,2.3,Iris-virginica
6.3,2.5,5.0,1.9,Iris-virginica
6.5,3.0,5.2,2.0,Iris-virginica
6.2,3.4,5.4,2.3,Iris-virginica
5.9,3.0,5.1,1.8,Iris-virginica
```
```
cut -d ',' -f 5 file.clean.csv | sort | uniq -c
```
```
   1 
  50 Iris-setosa
  48 Iris-versicolor
  50 Iris-virginica
 ```
# Question 3: Find a sequence

Find how many lines in the data file 'test.fastq.gz' start with "TGCAG" and end with "GAG". Describe your work.

Since I am dealing with a fastq.gz compressed file I piped the ```zgrep``` command into the ```wc``` command. The ```zgrep``` command is specifically designed to search this file type without messing up the compression. In this case, I am asking the command to search the file for strings that begin with "TGCAG" and end with "GAG". Then ```wc -l``` counts the number of lines that match this request. 

```
zgrep '^TGCAG.*GAG$' file.tgz | wc -l
```
```    
44
```

# Question 4: Find a sequence chunk 

Using ```grep``` and other tools if necessary find all lines that contain the sequence "AAAACCCC" and 
for each print that line, the line above it, and two lines below it (so that a 4-line chunk around each search 
hit is printed). Describe your work.

Similar to before I used the ```zgrep``` command since I am dealing with a compressed .gz file. I used it to locate all lines containing the equence "AAAACCCC". I then requested that it print the line immeidately before and the two lines after. In this case, the argument ```-B``` indicates before (each matching line in the output) and ```-A``` indicates after (each matching line in the output). 

```
zgrep -B 1 -A 2 'AAAACCCC' file.tgz
```
```
@32082_przewalskii.98 GRC13_0027_FC:4:1:5669:1669 length=74
TGCAGAATAGATAGGAAACGTTTTGGCGCTGTAGACATTAAAACCCCAGTAGGACACGGGTATCACAACGTACA
+32082_przewalskii.98 GRC13_0027_FC:4:1:5669:1669 length=74
IIIIIIIIIIIIIIIIIIHIHIIIIIIIIGIIIGIIIIIIHIIIIIIIHIIIIHIIIIIIEHIHHIIIIICIHI
--
@33413_thamno.59 GRC13_0027_FC:4:1:5000:1620 length=74
TGCAGTGGATCGAAAACCCCGAGGCTCAAGGTCACGCCACCGTCTTCGTGGCCAAGTTCTTCGGCCGCGCCGGC
+33413_thamno.59 GRC13_0027_FC:4:1:5000:1620 length=74
IIIIIIIIIIIIIIIIIIIIDHIIHHIIIIIEIBGBGGGIIHEHHHIEBBHHIEGGDGIGGHAEFDBFBDDB?D
```
