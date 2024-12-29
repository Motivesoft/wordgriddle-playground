# wordgriddle-playground
Experiments with word grids


# Notes

## Selections

### Validity
* A valid letter, during selection, is not already selected AND adjacent to the previous letter in the selection
* Being adjacent is judged as cell ```A``` being no more than one row _and_ column from cell ```B```
* The ```distance``` between ```A``` and ```B``` is the max difference between their ```row``` and ```column``` values
* ```A``` and ```B``` have an ```index``` from the top left of the grid, starting at ```0```
* The grid is square and has a length/width value of ```gridSize```
* ```column``` is ```index % gridSize```
* ```row``` is ```( index - column ) / gridSize``` (subtracting the column to arrive at an integer value)
* ```distance``` is ```MAX( ABS( A.column - B.column ), ABS( A.row - B.row ) )```

### Rules
* If ```distance``` is ```1``` and the new cell is not already part of the selection
  * add the cell to the selection
  * mark it selected and draw a line from the previous cell
  * update 'lastCell' so we know when we've moved to a different cell
* If the new cell is part of the selection and represents a step backwards from the previous selection
  * remove the topmost cell from the list
  * mark that cell as unselected
  * undraw the selection line from between the two cells
  * update 'lastCell' so we know when we've moved to a different cell
* Otherwise ignore the mouse move

# Ideas
* Make the letters slightly less selectable during a selection
  * ignore moves around the edge - test for being within (e.g.) 75% of the centre of each tile