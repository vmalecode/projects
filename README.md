# Finding Anagrams Using C

CS5008 Assignment 7 Documentation

### Overview

1. program description and general summary  
  * Program uses hashtable to find anagrams. It can be modified to search for individual anagrams
2. compile/run commands  
  * make all
  * make run
3. Example input/output  
  * See below
4. Files  
  * hashtable.c is the hashtable structure
  * anagram.c is the anagram structure
  * main.c runs the program
  * test_main.cc is the unit tests for the functions in the data structures
  * words.txt is the data target
  * readme.md is this file

5. Libraries  
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
```

### Executing program

* Terminal commands and output: 
```
(base) user1@desktop:~/nu/avmale_CS5008/a7$ make all
gcc -g Hashtable.c Main.c Anagram.c Assert007.c -o main
(base) user1@desktop:~/nu/avmale_CS5008/a7$ make run
./main
Read 432335 rows 
roaches rechaos oraches choreas 
tranche rechant chanter cathern 
terebra tabrere rebater bartree 
sarcine cerasin carnies arsenic arcsine 
manilas malians lamians animals almains 
salicet latices laciest elastic castile astelic alectis 
sidearm sedarim misread mardies admires 
tapered retaped readept predate padtree adepter 
roadmen omander mandoer madrone 
rentage reagent negater greaten grantee 
sledger redlegs ledgers gelders 
teleman manteel leetman leatmen entelam 
rereads redsear redears readers dreares 
singled engilds eldings dingles 
salited distale dilates details 
remiped impeder epiderm demirep 
steeled sleeted seedlet deletes 
relayed redelay layered delayer 
noticed deontic ctenoid condite 
terrace retrace recrate caterer 
scoriae oracies coraise caserio cariose 
tacrine nacrite crinate citrean certain ceratin centiar cantier 
scleral recalls cellars callers 
velaric valeric clavier claiver caviler caliver 
rebates bestare berates beaters 
troadic dartoic carotid arctoid 
tarpeia patriae pateria apteria 
bestian bestain besaint basinet banties antibe
```
Output is shortened for brevity.
The output can be searched using grep:
```
(base) user1@desktop:~/nu/avmale_CS5008/a7$ ./main | grep 'arrest'
treasr terras tarres starer sartre raters raster rarest astrer arrest 
```
## Valgrind

Valgrind report
```
(base) user1@desktop:~/nu/avmale_CS5008/a7$ valgrind ./main --leak-check=full
==37552== Memcheck, a memory error detector
==37552== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==37552== Using Valgrind-3.17.0 and LibVEX; rerun with -h for copyright info
==37552== Command: ./main --leak-check=full
==37552==  
==37552== 
==37552== HEAP SUMMARY:
==37552==     in use at exit: 0 bytes in 0 blocks
==37552==   total heap usage: 1,297,010 allocs, 1,297,010 frees, 79,461,301 bytes allocated
==37552== 
==37552== All heap blocks were freed -- no leaks are possible
==37552== 
==37552== For lists of detected and suppressed errors, rerun with: -s
==37552== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

## Test Report

Test compile and execution:
```
(base) user1@desktop:~/nu/avmale_CS5008/a7$ make test_suite 
-e ===========================
Building the test suite
-e ===========================
g++ -o test_suite Hashtable.o Assert007.o Anagram.o test_main.o \
	 -L/home/user1/lib/gtest -lgtest -lpthread
-e ====================================
Run tests by running ./test_suite
-e ====================================

(base) user1@desktop:~/nu/avmale_CS5008/a7$ ./test_suite 
[==========] Running 6 tests from 2 test cases.
[----------] Global test environment set-up.
[----------] 3 tests from Hashtable
[ RUN      ] Hashtable.CreateHashtable
[       OK ] Hashtable.CreateHashtable (0 ms)
[ RUN      ] Hashtable.DestroyHashtable
[       OK ] Hashtable.DestroyHashtable (0 ms)
[ RUN      ] Hashtable.Put
[       OK ] Hashtable.Put (0 ms)
[----------] 3 tests from Hashtable (0 ms total)

[----------] 3 tests from Anagram
[ RUN      ] Anagram.CreateAnagram
[       OK ] Anagram.CreateAnagram (0 ms)
[ RUN      ] Anagram.AddWordToAnagram
[       OK ] Anagram.AddWordToAnagram (0 ms)
[ RUN      ] Anagram.CreateWordNode
[       OK ] Anagram.CreateWordNode (0 ms)
[----------] 3 tests from Anagram (0 ms total)

[----------] Global test environment tear-down
[==========] 6 tests from 2 test cases ran. (0 ms total)
[  PASSED  ] 6 tests.

```

## Other Notes
Use this code to add functionality to search for individual words in terminal:  
```
char input[45];
while(1 == 2){
printf("Enter zzz to exit:\n");
printf("Enter word to search: ");
fgets(input, 45, stdin);

int a = sizeof(input);
SortWord(input);
if(strcmp(input + 1,"zzz") == 0){
    printf("Terminating\n");
    return 0;
}
searchAnagram = Get(ht, input + 1);
if(searchAnagram == NULL){
    printf("No Anagrams found \n");
}
else{
    PrintAnagram(searchAnagram);
}
}
```

