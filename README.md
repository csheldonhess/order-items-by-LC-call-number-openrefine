# order-items-by-LC-call-number-openrefine
An OpenRefine recipe that puts items in order by call number, even if the spacing is inconsistent (e.g. call numbers in the format AB123 and also AB 123).

TODO: Make it only add a _single_ space into the call number. (E.g. *AB123 .C23* should not become *AB 123 .C 23*)

Here's what the list of operations looks like, if you want to recreate it yourself, rather than pasting in an entire recipe of dubious origin:
- Text transform on cells in column `Call Number` using expression grel:`value.replace(/(\p{IsAlphabetic})(?=\d)/,'$1 ')`
- Create column `Full num (not for sorting)` at index 3 based on column `Call Number` using expression grel:`value.partition(' ')[2].trim()`
- Create column `Call Letter` at index 3 based on column `Call Number` using expression grel:`value.partition(' ')[0].trim()`
- Create column `Letter2` at index 5 based on column `Full num (not for sorting)` using expression grel:`value.split(' ')[1].replace('.','').trim()`
- Create column `Num (for sorting)` at index 5 based on column `Full num (not for sorting)` using expression grel:`value.split(' ')[0].trim()`
- Remove column `Full num (not for sorting)`
- Reorder rows
- Remove column `Call Letter`
- Remove column `Num (for sorting)`
- Remove column `Letter2`

