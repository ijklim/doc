# Google Sheets functions

* `ISBLANK(A1)`

* `ISODD(A1)`

* Current cell `ADDRESS(ROW(), COLUMN())`, e.g. $A$100
* Current cell (relative) `ADDRESS(ROW(), COLUMN()), 4`, e.g. A100
* Sum `=SUM(INDIRECT(ADDRESS(2, COLUMN())):INDIRECT(ADDRESS(ROW()-1, COLUMN())))`

* Cell reference `INDIRECT(CONCAT("A", ROW()))`

* `INT(WEEKNUM(A1))`

* `AND(condition1, condition2)`

* Current cell = first cell in range

  * e.g. Range `C3:M10`, Current Cell = `C3`

  * Sample: `=AND(ISBLANK(B3), ISBLANK($A3) = FALSE)`, 2nd cell blank and 1st cell not blank

* Detect duplicate `=COUNTIF($C$3:$C$1000, $C3)>1`


