# Question 1: Get the data files 

Download the following data files from the internet using the curl command: 'http://eaton-lab.org/pdsb/test.fastq.gz'and 'http://eaton-lab.org/pdsb/iris-data-dirty.csv.' Use the 'less' or 'zless' commands to look at each file. Describe what these commands do. Finally, use the 'head' command to print the first 5 lines of the file 'iris-data-dirty.csv'.

I first downloaded both data files using the curl command. 

```
curl -L -o file.tgz http://eaton-lab.org/pdsb/test.fastq.gz
less file.tgz
```
```
file.tgz may be a binary file. See it anyway? Y
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
(previous)...
6.1,2.6,5.6,1.4,Iris-virginica
7.7,3.0,6.1,2.3,Iris-virginica
6.3,3.4,5.6,2.4,Iris-virginica
6.4,3.1,5.5,1.8,Iris-virginica
... (continued)
```
# Question 2: Clean the data 

Use grep, uniq, and sed for this question. Check that all of the species names are spelled correctly in the file 'iris-data-dirty.csv'. 
Also check for missing values stored as NA. Create a new file where mispelled names are replaced with the correct values, 
and lines with "NA" are excluded, and save it as 'iris-data-clean.csv'. Use cut, sort and uniq to list the number of 
data values there are for each species in the new cleaned data file. Describe your work.

# Question 3: Find a sequence

Find how many lines in the data file 'test.fastq.gz' start with "TGCAG" and end with "GAG". Describe your work.

# Question 4: Find a sequence chunk 

Using 'grep' and other tools if necessary find all lines that contain the sequence "AAAACCCC" and 
for each print that line, the line above it, and two lines below it (so that a 4-line chunk around each search 
hit is printed). Describe your work.

