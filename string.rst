===========
Bash String
===========

Introduction
============

String Methods
==============
Case
----
TR
::

  $ echo "$a" | tr '[:upper:]' '[:lower:]'
  hi all


AWK
::

  $ echo "$a" | awk '{print tolower($0)}'
  hi all


Bash 4.0
::

   $ echo "${a,,}"
   hi all


Perl
::

   $ echo "$a" | perl -ne 'print lc'
   hi all


Bash
::

  lc(){
    case "$1" in
        [A-Z])
        n=$(printf "%d" "'$1")
        n=$((n+32))
        printf \\$(printf "%o" "$n")
    esac
  }
  word="ABX"
  for((i=0;i<${#word};i++))
  do
    ch="${word:$i:1}"
    lc "$ch"
  done
 
Strip
-----
String startswith or endswith
-----------------------------
Search
------
Replace substring
-----------------
Split
-----
join array into strings
-----------------------
Slicing
=======
format
======
Conditionals With String
========================
