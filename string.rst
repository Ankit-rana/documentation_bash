===========
Bash String
===========

Introduction
============

String Methods
==============
Case
----

* TR
::

  $ echo "$a" | tr '[:upper:]' '[:lower:]'
  hi all


* AWK
::

  $ echo "$a" | awk '{print tolower($0)}'
  hi all


* Bash 4.0
::

   $ echo "${a,,}"
   hi all


* Perl
::

   $ echo "$a" | perl -ne 'print lc'
   hi all


* Bash
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

* SED
removes all possible spaces at the end of the line
::

  sed 's/ *$//' file
  
* ECHO AND WC
The echo command used the option -n to avoid adding a return character and causing wc -m count an additional character.
::

  FOO=' test test test '
  echo -e "length(FOO)==$(echo -ne "${FOO}" | wc -m)"      # > length(FOO)==16
::

  #How to remove all whitespace (denoted by [:space:] in tr)
  FOO_NO_WHITESPACE="$(echo -e "${FOO}" | tr -d '[:space:]')"
  echo -e "FOO_NO_WHITESPACE='${FOO_NO_WHITESPACE}'"       # > FOO_NO_WHITESPACE='testtesttest'
  echo -e "length(FOO_NO_WHITESPACE)==$(echo -ne "${FOO_NO_WHITESPACE}" | wc -m)"    # > length(FOO_NO_WHITESPACE)==12
::
  
  #How to remove leading whitespace only
  FOO_NO_LEAD_SPACE="$(echo -e "${FOO}" | sed -e 's/^[[:space:]]*//')"     #'test test test '
::
  
  #How to remove trailing whitespace only
  FOO_NO_TRAIL_SPACE="$(echo -e "${FOO}" | sed -e 's/[[:space:]]*$//')"    #' test test test'
::

  #How to remove both leading and trailing spaces chain the seds
  FOO_NO_EXTERNAL_SPACE="$(echo -e "${FOO}" | sed -e 's/^[[:space:]]*//' -e 's/[[:space:]]*$//')"

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
