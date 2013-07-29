vocabulary.sh
=============

Fetches Vocabulary.com summaries, and formats them nicely for terms.

AGREEMENT:
Do whatever you want with this script, don't bother with including licence or anything.

Here is the script:
```
#!/bin/bash
curl -s "https://www.vocabulary.com/dictionary/autocomplete?search=$@" | perl -pe '
        s/<span[^>]*>([\w\s]*)<\/span>\s*<span[^>]*>([\w\s\p{P}]*)<\/span>/\n\e[36m\1:\t\e[0m \2\n/g;
        s/^\s+$//g; # Remove blank lines
' | perl -pe '
        # Remove all other junk.
        s/^<\/?(li)?(ol)?.*\n?//g;
'
```
