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
if s1 in s2 ?
::
  
  if [[ $s1 == *"$s2"* ]]
  then
    do something
  fi
shortest substring match
::
  
  ${string#substring}
longest substring match
::
  
  ${string##substring}
shortest substring match from right
::
  
  ${string%substring}
longest substring match from right
::
  
  ${string%%substring}
Replace substring
-----------------
replace first occurance of a substring
::
  #syntax : ${string/pattern/replacement}
  original_string='i love Suzi and Marry'
  string_to_replace_Suzi_with=Sara
  result_string="${original_string/Suzi/$string_to_replace_Suzi_with}"
Split
-----
returns a list of substrings separated by the given delimiter(in most cases a space)
::
  arr=($line)
  or
  read -a arr <<<$line
  or
  IFS=', ' read -r -a array <<< "$string"
join array into strings
-----------------------
opposite of splitting, joins the elements in the given list together using the string as the delimiter
::
  function join_by { local IFS="$1"; shift; echo "$*"; }
  join_by , a "b c" d #a,b c,d
  join_by / var local tmp #var/local/tmp
  join_by , "${FOO[@]}" #a,b,c
Slicing
=======
The "slice" syntax is a handy way to refer to sub-parts of sequences -- typically strings and lists
::
  
  ${string:position:length}
format
======
To put together the strings and variable
::

   name="ankit"
   echo "nice boy $name"
Conditionals With String
========================
On contrary to comparision with number where we use operator like -eq, strings are compared with '=='
::

  name="ankit"
  if [[ $name == "dana" ]]
  then
   do something
  elif [[ $name == "rana" ]]
  then
   do something
  else
   do something
  fi
    
