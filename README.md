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

## 02 Structure


