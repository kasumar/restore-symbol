# restore-symbol

A reverse engineering tool to restore stripped symbol table for iOS app.

Example: restore symbol for Alipay
![](https://raw.githubusercontent.com/tobefuturer/restore-symbol/master/picture/after_restore.jpeg)


## How to use
- 1. Download source code and compile 

```

git clone --recursive https://github.com/tobefuturer/restore-symbol.git
cd restore-symbol && make
./restore-symbol

```

- 2. Search block symbol in IDA to get json symbol file, using script([`search_oc_block/ida_search_block.py`](https://github.com/tobefuturer/restore-symbol/blob/master/search_oc_block/ida_search_block.py)) .

![](http://blog.imjun.net/2016/08/25/iOS%E7%AC%A6%E5%8F%B7%E8%A1%A8%E6%81%A2%E5%A4%8D-%E9%80%86%E5%90%91%E6%94%AF%E4%BB%98%E5%AE%9D/ida_result_position.png)

![](http://blog.imjun.net/2016/08/25/iOS%E7%AC%A6%E5%8F%B7%E8%A1%A8%E6%81%A2%E5%A4%8D-%E9%80%86%E5%90%91%E6%94%AF%E4%BB%98%E5%AE%9D/ida_result_sample.jpg)

- 3. Use command line tool(restore-symbol) to inject oc method symbols and block symbols into mach o file.

```

./restore-symbol /pathto/origin_mach_o_file -o /pathto/mach_o_with_symbol -j /pathto/block_symbol.json

```


## Command Line Usage 
```
Usage: restore-symbol -o <output-file> [-j <json-symbol-file>] <mach-o-file>

  where options are:
        -o <output-file>           New mach-o-file path
        --disable-oc-detect        Disable auto detect and add oc method into symbol table,
                                   only add symbol in json file
        -j <json-symbol-file>      Json file containing extra symbol info, the key is "name","address"
                                   like this:

                                        [
                                         {
                                          "name": "main",
                                          "address": "0xXXXXXX"
                                         },
                                         {
                                          "name": "-[XXXX XXXXX]",
                                          "address": "0xXXXXXX"
                                         },
                                         ....
                                        ]

```
