# txt_transformer

## 01 Background
In many scenarios, large table data will be saved in txt format. The needed parts would be extracted from the txt and converted into csv format for subsequent operations once needed. txt_transformer provides such a tool to read out the data in txt and write it to csv files.

The data input would be like in this format:

<img width="391" alt="image" src="https://user-images.githubusercontent.com/86709726/212458106-22f8f556-2a73-41dc-8d99-526f94c5016b.png">

That is, a txt file with content consisting of lines in string format. And the function would read these lines one by one and next extract their information. These strings would be splitted under an unified format set by the command.

The command would be like: 
```
0,12;12,12;24,12;
```
This means we want for each single line in the txt, we only want three: the language block of length 12 from digit 0, block of length 12 from digit 12 and the block of length 12 from digit 24. By replacing all useless spaces (before or after content) with empty, the input above would be splitted into:

<img width="610" alt="image" src="https://user-images.githubusercontent.com/86709726/212458498-c25aa96f-89c6-4956-b02a-a13ea71a5877.png">

In contrast with replacing characteristic signals (characters) with commas and semicolons hence writing into csv, the txt_transformer rewrite csv basing on the command input. You need to input the path (filename included) first and input the command next, hence creating a table showed as above.


## 02 Structure & Functions
txt_transformer generate the csv basing on commands (normally input in string for a convenience), hence, a data structure to store the command it is needed. We can't anticipate how many columns would be needed, hence I built a linked list to store so. For each node, containing information include:
```c
typedef struct comStr 
{
    int start;                  // the digit of the head of the block,
    int length;                 // the length of the block,
    int count;                  // the index number of the node,
    struct comStr *next;        // the next node
} LinkList0;
```
We also need to provide a linkedlist to store sentence, and next to split them basing on the commmand one by one, lastly write them into csv.
```c
typedef struct infoStr 
{
    char* content;
    struct infoStr *next;
} LinkList1;
```

### 01 openTxt
openTxt is a function open the txt file by locating the file name input (fname), read the content inside and next extract information out.
```c
static char *openTXT (char *fname);
```
### 02 split
split is a function used to split a string basing on the sperator, meanwhile would count the number of blocks splitted (stored in num) and next return the splitted array (stored in **result), just like the split do in python.
```c
static void split (char *source, char *seperator, char **result, int *num);
```

### 03 cmdLink
This function is to build a link of command node basing on the array input generated in function split.
```c
static LinkList0 *cmdLink (char *command, char *sep);
```

### 04 substring
This function is to crop a substring basing on a source string given, just like ```src[start+1:start+len+1:]``` do in python.
```c
static char* substring (char *src, int start, int length);
```
### 05 genereateRow
This function is to generate a row basing on the sourceLine (string) and the command. 
```c
static char* genereateRow (char* srcLine, LinkList0 *currLink);
```
### 06 showNodes
This function is to present the nodes one by one in the command linked list. 
```c
static void showNodes (LinkList0 *currLink);
```
### 07 freeNodes
This function is to free the momory allocated by the nodes one by one in the command linked list.
```c
static void freeNodes (LinkList0 *currLink);
```
### 08 writeCSV
This function is to write the CSV down, the csv's name would be ```result.csv```.
```c
static void writeCSV (char *srcText, char* command);
```





