---
title: Linux shell script
date: 2022-01-01
hide:
    - tags
tags:
    - 'shell'
---


# Shell script

## Loop line of txt file

```shell
while read p; do
    echo "$p" 
    
    ## trim white space
    trimmed_line="$(echo -e "${p}" | tr -d '[:space:]')"
   
    newfilename=$trimmed_line.sql
    
    ## append to template.sql and create new file
    echo "\set var $log_hash" | cat - template.sql >  "sql/$newfilename"	
  
  
done <file.txt
```
