# ctkn
Ctkn: Light-weight C parsing module for Perl.

C-style tokenizer which removes /* C comments */,
does string tokenization, and identifier tokenization.
The raw materials are here for processing tokens like ++, +=, ==, etc.,
but at present those will be interpreted as two tokens (of type 'id').

I don't have time to learn Yacc and Lex (or their gnu equivs),
or learn a rich Perl module.
I just wanted something quick and dirty,
but which handles certain common lexical constructs,
like strings and comments.

To run unit tests:
```
$ perl -e 'use strict;use warnings;use Carp;require "ctkn.pl";ctkn_UT();'
```

With debug:
```
$ perl -e 'use strict;use warnings;use Carp;require "ctkn.pl";ctkn_UT("d");'
```

Normal public API functions:
```
#   ctkn_new(option_string) - create new instance of parser.
#     option_string: one or more option characters:
#       c - convert \r, \n, and \t in strings to their control characters.
#       C - Only recognize C comments /*...*/ (tokenize // comments).
#       d - debug prints enabled.
#     Returns: handle to parser instance.
#
#   ctkn_input(ctkn, input_line, loc_string) - feed the parser a line of text
#       to be parsed.
#     ctkn - handle returned by ctkn_new().
#     input_line - line of C code to be parsed.
#     loc_string - nominally file name and line number of input_line.
#
#   ctkn_eof(ctkn) - tell parser the end-of-file was reached.
#     ctkn - handle returned by ctkn_new().
#
#   ctkn_num(ctkn) - returns number of tokens parsed.
#     ctkn - handle returned by ctkn_new().
#
#   ctkn_vals(ctkn) - returns reference to array of token values (see example).
#     ctkn - handle returned by ctkn_new().
#
#   ctkn_types(ctkn) - returns reference to array of token types (see example).
#                      Types are "id", "dqstring" (double quotes), and
#                      "sqstring" (single quotes).
#     ctkn - handle returned by ctkn_new().
#
#   ctkn_locs(ctkn) - returns reference to array of locations for input
#       with column number added (see example).
#     ctkn - handle returned by ctkn_new().
#
#   ctkn_dump(ctkn) - produce a human-readable form of the tokens.
#     ctkn - handle returned by ctkn_new().
#     Returns: string containing dump.
#
# Example:
#   See the function "ctkn_EXAMPLE" at the end of this file.  To run it:
#     perl -e 'require "ctkn.pl";ctkn_EXAMPLE();'
```
