# Google Sheets functions

* `ISBLANK(A1)`

* `ISODD(A1)`

* Cell reference `INDIRECT(CONCAT("A", ROW()))`

* `INT(WEEKNUM(A1))`

* `AND(condition1, condition2)`

* Current cell = first cell in range

  * e.g. Range `C3:M10`, Current Cell = `C3`

  * Sample: `=AND(ISBLANK(B3), ISBLANK($A3) = FALSE)`, 2nd cell blank and 1st cell not blank

* Detect duplicate `=COUNTIF($C$3:$C$1000, $C3)>1`
