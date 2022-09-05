# Migration to Androidx
### this is a python script to migrate from ***Support Library Class*** to ***Androidx Class***

Migrate to Androidx script
in case the automatic way to migrate from support library class to androidx doesn't work well you can run this script to replace every old package in the project with androidx packages

```
# Driver functions
import os
import pandas as pd
import csv
```

These are the the directory path to the project we want change and the mappings in csv format here the link to download it (https://developer.android.com/jetpack/androidx/migrate/class-mappings)

```
# here change the path according to your project
project_path="C:\\Users\\Sliman2015\\Downloads\\my_code"
csv_path="androidx-class-mapping.csv"
fileExtension = [".xml",".java",".kt"]
dicts={}
```

Read the csv file
Read the csv file of the support library class and androidx class

```
data = pd.read_csv(csv_path)
df = pd.DataFrame(data)
df.head()
```
Support Library class	Android X class
0	android.arch.core.executor.AppToolkitTaskExecutor	androidx.arch.core.executor.AppToolkitTaskExec...
1	android.arch.core.executor.ArchTaskExecutor	androidx.arch.core.executor.ArchTaskExecutor
2	android.arch.core.executor.DefaultTaskExecutor	androidx.arch.core.executor.DefaultTaskExecutor
3	android.arch.core.executor.JunitTaskExecutorRule	androidx.arch.core.executor.JunitTaskExecutorRule
4	android.arch.core.executor.TaskExecutor	androidx.arch.core.executor.TaskExecutor
 
Put the directory path and the files's name with extension .xml and .java and .kt in dictionnary to access them in the next step.
```
dicts={'path1':['file1', 'file2', 'file3', ...],
       path2:[....]
       ...}
```

```
if __name__ == "__main__":
    for (root,dirs,files) in os.walk(project_path):
        list_files=[]
        for file in files:
            if file.endswith(tuple(fileExtension)):
                list_files.append(file)
        if len(list_files)>0:
            dicts[root] = list_files
```

Replace and overwrite the changes with loops
Replace the old packages with the androidx packages in file from our dictionnary using loop, and overwrite the same file with the replaced text so the changes will be saved.

```
for path in dicts.keys():
    for mFile in dicts[path]:
        # Read in the file
        mFile_path = path+"\\"+mFile
        with open(mFile_path, 'r', encoding="utf8") as file :
            filedata = file.read()
            #iterate over rows in dataframe
            for index, row in df.iterrows():
                # Replace the target string
                filedata = filedata.replace(row['Support Library class'], row['Android X class'])
                
        #overwrite the file with filedata which the replaced text
        with open(mFile_path, 'w', encoding="utf8") as file :
            file.write(filedata)
print("the migration to Androidx done ;)")
```
the migration to Androidx done ;)
