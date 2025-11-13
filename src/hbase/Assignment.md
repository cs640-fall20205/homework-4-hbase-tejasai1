# Assignment 4 - Columnar Databases and HBase

## 7in7 - HBase - Day 1

### Part 1 - Interactive Reading

Read Day 1 and work through the examples in the chapter.
Save your final database in a directory `day1` as follows.

```
./save.bash wiki day1
```

You can use the same script to save your database between work sessions.
But you cannot save over an existing save. So use temporary names like:
`day1a`, `day1b`, etc. You can use the `./load.bash` script to restore
an empty database from a saved state.

Here are some additional tips:

* Skip **Configuring HBase**.
* Begin with the last command on p57: `version`.
* p59 - Do not run these in the shell, which is Ruby.
    These are illustrative examples in python.
* p64 - The last example is split over 2 lines. `hbase>` and `hbase*` are
    not part of the command.
* I have not been able to use the colons inside of quotes in the hbase commands. If they don't work with the colon, try them without.
* The command to allow unlimited  versions is:

`alter 'wiki', {NAME => 'text', VERSIONS => 2147483647 }`

### Part 2 - 7in7 - HBase Day 1 - Find

1. Figure our how to use the shell to do the following:

    * Delete individual column values in a row:

        ```
         delete 'table_name', 'row_key', 'column_family:qualifier'
         example from Day 1 practice : delete 'wiki', 'Home', 'text:content'
        ```

    * Delete an entire row

        ```
        deleteall 'table_name', 'row_key'
        General example: deleteall 'users', 'user1'
        ```


2. Bookmark the HBase API documentation for the version of HBase you’re using.

    ```
    https://hbase.apache.org/apidocs/index.html
    ```

### Part 3 - Create a family database

#### Step 1 - Create an hbase table that represents a family.

Specifically, you should have column families for the following:
* personal information: names of family members and birthdays
* favorites: foods and vacation locations
* location information: addresses including street, city, state, and zip. and phone numbers

Place the Hbase code to create the families below:
```
create 'families', 'personal info', 'favourites', 'location'
```

#### Step 2 - Load five rows of data.
Make sure to have at least one row with more than one favorite food and at least one row with more than one favorite vacation location. Place the Hbase code below:
```
family number 1:
hbase(main):011:0> put 'families', 'Teja', 'personal info:name', 'Tejasaikola'
0 row(s) in 0.0160 seconds

hbase(main):012:0> put 'families', 'Teja', 'personal info:birthday', '06-06-2000'
0 row(s) in 0.0090 seconds

hbase(main):013:0> put 'families', 'Teja', 'favourites:food', 'pizza'
0 row(s) in 0.0140 seconds

hbase(main):014:0> put 'families', 'Teja', 'favourites:vacation', 'Hawaii'
0 row(s) in 0.0070 seconds

hbase(main):015:0> put 'families', 'Teja', 'location:street', '123 Maple st'
0 row(s) in 0.0090 seconds

hbase(main):016:0> put 'families', 'Teja', 'location:state', 'MA'
0 row(s) in 0.0110 seconds

hbase(main):017:0> put 'families', 'Teja', 'location:zip', '01020'
0 row(s) in 0.0060 seconds

hbase(main):018:0> put 'families', 'Teja', 'location:phone', '413-575-7121'
0 row(s) in 0.0070 seconds

family number 2:
hbase(main):020:0> put 'families', 'sandy', 'personal info:name', 'sandeep'
0 row(s) in 0.0120 seconds

hbase(main):021:0> put 'families', 'sandy', 'personal info:birthday', '08-07-2000'
0 row(s) in 0.0130 seconds

hbase(main):022:0> put 'families', 'sandy', 'favourites:food', 'fries'
0 row(s) in 0.0130 seconds

hbase(main):023:0> put 'families', 'sandy', 'favourites:food', 'burgers'
0 row(s) in 0.0140 seconds
put 'families', 'sandy', 'favourites:vacation', 'florida'
0 row(s) in 0.0170 seconds
hbase(main):025:0> put 'families', 'sandy', 'location:street', '123 Maple st'
0 row(s) in 0.0100 seconds

hbase(main):026:0> put 'families', 'sandy', 'location:city', 'chicopee'
0 row(s) in 0.0070 seconds

hbase(main):027:0> put 'families', 'sandy', 'location:state', 'MA'
0 row(s) in 0.0110 seconds

hbase(main):028:0> put 'families', 'sandy', 'location:zip', '01020'
0 row(s) in 0.0100 seconds

hbase(main):029:0> put 'families', 'sandy', 'location:phone', '413-555-2345'
0 row(s) in 0.0140 seconds

family number 3:
hbase(main):030:0> put 'families', 'ramu', 'personal info:name', 'ramesh'
0 row(s) in 0.0200 seconds

hbase(main):031:0> put 'families', 'ramu', 'personal info:birthday', '01-02-2000'
0 row(s) in 0.0090 seconds

hbase(main):032:0> put 'families', 'ramu', 'favourites:food', 'ice cream'
0 row(s) in 0.0100 seconds

hbase(main):033:0> put 'families', 'ramu', 'favourites:vacation', 'paris'
0 row(s) in 0.0070 seconds

hbase(main):034:0> put 'families', 'ramu', 'favourites:vacation', 'Disney world'
0 row(s) in 0.0090 seconds
hbase(main):035:0> put 'families', 'ramu', 'location:street', '1215 wilbraham rd'
0 row(s) in 0.0080 seconds

hbase(main):036:0> put 'families', 'ramu', 'location:city', 'springfield'
0 row(s) in 0.0090 seconds

hbase(main):037:0> put 'families', 'ramu', 'location:state', 'MA'
0 row(s) in 0.0100 seconds

hbase(main):038:0> put 'families', 'ramu', 'location:zip', '01119'
0 row(s) in 0.0110 seconds

hbase(main):039:0> put 'families', 'ramu', 'location:phone', '413-123-4567'
0 row(s) in 0.0070 seconds

family number 4:
hbase(main):040:0> put 'families', 'suri', 'personal info:name', 'suresh'
0 row(s) in 0.0080 seconds

hbase(main):041:0> put 'families', 'suri', 'personal info:birthday', '12-09-1999'
0 row(s) in 0.0070 seconds

hbase(main):042:0> put 'families', 'suri', 'favourites:food', 'pizza'
0 row(s) in 0.0070 seconds

hbase(main):043:0> put 'families', 'suri', 'favourites:vacation', 'New york'
0 row(s) in 0.0090 seconds

hbase(main):044:0> put 'families', 'suri', 'location:street', '1215 wilbraham rd'
0 row(s) in 0.0080 seconds
hbase(main):045:0> put 'families', 'suri', 'location:city', 'springfield'
0 row(s) in 0.0070 seconds

hbase(main):046:0> put 'families', 'suri', 'location:state', 'MA'
0 row(s) in 0.0100 seconds

hbase(main):047:0> put 'families', 'suri', 'location:zip', '01119'
0 row(s) in 0.0060 seconds

hbase(main):048:0> put 'families', 'suri', 'location:phone', '413-678-9876'
0 row(s) in 0.0100 seconds

family number 5:
hbase(main):049:0> put 'families', 'prabha', 'personal info:name', 'prabhas'
0 row(s) in 0.0080 seconds

hbase(main):050:0> put 'families', 'prabha', 'personal info:birthday', '10-21-1978'
0 row(s) in 0.0130 seconds

hbase(main):051:0> put 'families', 'prabha', 'favourites:food', 'pasta'
0 row(s) in 0.0080 seconds

hbase(main):052:0> put 'families', 'prabha', 'favourites:vacation', 'california'
0 row(s) in 0.0100 seconds

hbase(main):053:0> put 'families', 'prabha', 'location:street', '123 maple st'
0 row(s) in 0.0090 seconds

hbase(main):054:0> put 'families', 'prabha', 'location:city', 'chicopee'
0 row(s) in 0.0110 seconds

hbase(main):055:0> put 'families', 'prabha', 'location:state', 'MA'
0 row(s) in 0.0070 seconds

hbase(main):056:0> put 'families', 'prabha', 'location:zip', '01020'
0 row(s) in 0.0120 seconds

hbase(main):057:0> put 'families', 'prabha', 'location:phone', '413-666-1234'
0 row(s) in 0.0090 seconds
```

#### Step 3 – Create HBase queries for the items below.

Place the Hbase code **and the results** after each query.

**Query 1:** Get complete information for a specific family member.
```
hbase(main):058:0> get 'families', 'Teja'
COLUMN          CELL
 favourites:foo timestamp=1762983719059, value=pizza
 d
 favourites:vac timestamp=1762983759561, value=Hawaii
 ation
 location:phone timestamp=1762984332622, value=413-575-7
                121
 location:state timestamp=1762983898428, value=MA
 location:stree timestamp=1762983851474, value=123 Maple
 t               st
 location:zip   timestamp=1762983963495, value=01020
 personal info: timestamp=1762983479348, value=06-06-200
 birthday       0
 personal info: timestamp=1762983400120, value=Tejasaiko
 name           la
8 row(s) in 0.0450 seconds
```

**Query 2:** View only personal information for all family members.
```
 hbase(main):059:0> scan 'families', {COLUMNS => 'personal info'}
ROW             COLUMN+CELL
 Teja           column=personal info:birthday, timestamp
                =1762983479348, value=06-06-2000
 Teja           column=personal info:name, timestamp=176
                2983400120, value=Tejasaikola
 prabha         column=personal info:birthday, timestamp
                =1762988495928, value=10-21-1978
 prabha         column=personal info:name, timestamp=176
                2988466111, value=prabhas
 ramu           column=personal info:birthday, timestamp
                =1762987032910, value=01-02-2000
 ramu           column=personal info:name, timestamp=176
                2987003175, value=ramesh
 sandy          column=personal info:birthday, timestamp
                =1762985992306, value=08-07-2000
 sandy          column=personal info:name, timestamp=176
                2985152443, value=sandeep
 suri           column=personal info:birthday, timestamp
                =1762987610160, value=12-09-1999
 suri           column=personal info:name, timestamp=176
                2987564608, value=suresh
5 row(s) in 0.0570 seconds

```

**Query 3:** Get the name, favorite foods, and vacation locations for one family member.
```
 hbase(main):060:0> get 'families', 'prabha', {COLUMNS => ['personal info:name', 'favourites']}
COLUMN          CELL
 favourites:foo timestamp=1762988741239, value=pasta
 d
 favourites:vac timestamp=1762988759157, value=californi
 ation          a
 personal info: timestamp=1762988466111, value=prabhas
 name
3 row(s) in 0.0150 seconds
```

**Query 4:** Get a range of at least two family members.
```
hbase(main):061:0> scan 'families', {STARTROW => 'Teja', STOPROW => 'ramu'}
ROW             COLUMN+CELL
 Teja           column=favourites:food, timestamp=176298
                3719059, value=pizza
 Teja           column=favourites:vacation, timestamp=17
                62983759561, value=Hawaii
 Teja           column=location:phone, timestamp=1762984
                332622, value=413-575-7121
 Teja           column=location:state, timestamp=1762983
                898428, value=MA
 Teja           column=location:street, timestamp=176298
                3851474, value=123 Maple st
 Teja           column=location:zip, timestamp=176298396
                3495, value=01020
 Teja           column=personal info:birthday, timestamp
                =1762983479348, value=06-06-2000
 Teja           column=personal info:name, timestamp=176
                2983400120, value=Tejasaikola
 prabha         column=favourites:food, timestamp=176298
                8741239, value=pasta
 prabha         column=favourites:vacation, timestamp=17
                62988759157, value=california
 prabha         column=location:city, timestamp=17629888
                32307, value=chicopee
 prabha         column=location:phone, timestamp=1762988
                891050, value=413-666-1234
 prabha         column=location:state, timestamp=1762988
                850433, value=MA
 prabha         column=location:street, timestamp=176298
                8809320, value=123 maple st
 prabha         column=location:zip, timestamp=176298887
                0677, value=01020
 prabha         column=personal info:birthday, timestamp
                =1762988495928, value=10-21-1978
 prabha         column=personal info:name, timestamp=176
                2988466111, value=prabhas
2 row(s) in 0.0360 seconds
```

**Query 5:** Get the addresses for all family members.
```
hbase(main):062:0> scan 'families', {COLUMNS => ['location:street', 'location:city', 'location:state', 'location:zip']}
ROW             COLUMN+CELL
 Teja           column=location:state, timestamp=1762983
                898428, value=MA
 Teja           column=location:street, timestamp=176298
                3851474, value=123 Maple st
 Teja           column=location:zip, timestamp=176298396
                3495, value=01020
 prabha         column=location:city, timestamp=17629888
                32307, value=chicopee
 prabha         column=location:state, timestamp=1762988
                850433, value=MA
 prabha         column=location:street, timestamp=176298
                8809320, value=123 maple st
 prabha         column=location:zip, timestamp=176298887
                0677, value=01020
 ramu           column=location:city, timestamp=17629874
                02653, value=springfield
 ramu           column=location:state, timestamp=1762987
                434464, value=MA
 ramu           column=location:street, timestamp=176298
                7366946, value=1215 wilbraham rd
 ramu           column=location:zip, timestamp=176298746
                9369, value=01119
 sandy          column=location:city, timestamp=17629868
                48773, value=chicopee
 sandy          column=location:state, timestamp=1762986
                877770, value=MA
 sandy          column=location:street, timestamp=176298
                6809236, value=123 Maple st
 sandy          column=location:zip, timestamp=176298691
                9723, value=01020
 suri           column=location:city, timestamp=17629877
                41994, value=springfield
 suri           column=location:state, timestamp=1762987
                814892, value=MA
 suri           column=location:street, timestamp=176298
                7723208, value=1215 wilbraham rd
 suri           column=location:zip, timestamp=176298783
                1434, value=01119
5 row(s) in 0.0450 seconds
```

**Query 6:** Get the names of family members who like a specific favorite food (e.g., pizza).
```
hbase(main):066:0> scan 'families', {FILTER => "ValueFilter(=,'binary:pizza')", COLUMNS => ['favourites:food', 'personal info:name']}
ROW             COLUMN+CELL
 Teja           column=favourites:food, timestamp=176298
                3719059, value=pizza
 suri           column=favourites:food, timestamp=176298
                7657854, value=pizza
2 row(s) in 0.0490 seconds
```

**Query 7:** Create a vacation preference list with names.
```
hbase(main):067:0> scan 'families', {COLUMNS => ['personal info:name', 'favourites:vacation']}
ROW             COLUMN+CELL
 Teja           column=favourites:vacation, timestamp=17
                62983759561, value=Hawaii
 Teja           column=personal info:name, timestamp=176
                2983400120, value=Tejasaikola
 prabha         column=favourites:vacation, timestamp=17
                62988759157, value=california
 prabha         column=personal info:name, timestamp=176
                2988466111, value=prabhas
 ramu           column=favourites:vacation, timestamp=17
                62987111884, value=Disney world
 ramu           column=personal info:name, timestamp=176
                2987003175, value=ramesh
 sandy          column=favourites:vacation, timestamp=17
                62986427752, value=florida
 sandy          column=personal info:name, timestamp=176
                2985152443, value=sandeep
 suri           column=favourites:vacation, timestamp=17
                62987680570, value=New york
 suri           column=personal info:name, timestamp=176
                2987564608, value=suresh
5 row(s) in 0.0200 seconds
```

### Part 4 - 7in7 - Day 3 - Wrap Up

Read Day 3 - Wrap Up. Then answer the following.

1. List the pros of HBase as described in our text.

    ```
    *Robust scale-out architecture: hbase is designed to handle huge amounts of data like terabytes or more efficiently.
    *Rack awareness: it replicates data within and across datacenter racks, so that node failures can be handled gracefully and quickly
    *compression capabilities: it helps optimize storage and performance.
    ```

2. List the cons of HBase as described in our text.

    ```
    * hbase requires at least five nodes, not suitable for small scale problems
    * nonexpert documentation is limited, making it challenging for beginners.
    *hbase needs supporting infrastructure like Hadoop,Spark, which adds complexity
    ```


### 7in7 - Day 2 - OPTIONAL

OPTIONAL - You may safely skip Day 2.

This section contains a code-heavy example of loading a large amount
of data into your HBase database. If you feel like a challenge and are
interested, feel free to work through it.

If you do this section, please **do not** use ./save.bash to save
your database, because it may become very large.

So if you are ready for the challenge, below are some instructions to
help you along. Good luck!

1. Download and extract the source code for the text: https://pragprog.com/titles/pwrdata/seven-databases-in-seven-weeks-second-edition/

2. Drag the following files into 02_hbase/local/scripts on GitPod.
    * source_code/02_hbase/import_from_wikipedia.rb
    * source_code/02_hbase/create_wiki_schema.rb

3. Start your database.

4. Run the following to create the wiki table.

    ```
    ./shell.bash create_wiki_schema.rb
    ```

5. Now you should be able to run the command below.
    BEFORE YOU DO... be ready to press CTRL+C to stop the process. This
    command will load a lot of data very fast.

    ```
    curl https://dumps.wikimedia.org/enwiki/latest/enwiki-latest-pages-articles.xml.bz2 | bzcat | ./shell.bash import_from_wikipedia.rb
    ```

6. After it appears to be working, press CTRL+C to stop it.

7. Connect to your database.

8. Run the command below to count the number of
    rows in your 'wiki' table.

    ```
    count 'wiki'
    ```

    Copy and paste the output of this command below.

9. Run the command below to get information about your database's regions.

    ```
    scan 'hbase:meta',{FILTER=>"PrefixFilter('wiki')"}
    ```

    Copy and past the output of this command below.
