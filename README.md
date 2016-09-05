# Sudoku-Checker---SRMAUV
Program to checker Validity of Sudoku
#include <iostream.h>
#include<conio.h>

int sudoku[9][9];
int Check (int y[]);
int temp[9];

void print(int matrix[9][9]) {
  for (int i = 0; i < 9; i++){
    for (int j = 0; j < 9; j++)
      cout << matrix[i][j] << " ";
    cout << endl;
  }
  return;
}
// All the *check functions read the respective elements to a linear array and
//pass it to the check() function. Check function searches for multiple
//occurences of numbers, starting from the first element.

//Checks for duplications in each row
int RowCheck ( int x[9][9]) {
  for (int i=0; i<9; i++) {
    for (int j= 0; j<9; j++)
      temp[j] = x[i][j];

    if ( Check (temp) == 0 )
      return 0;
  }
  return 1;
}

//Main Check function
int Check (int y[9]) {
  int lineartemp;
  for (int i=0; i<9; i++) {
    lineartemp = y[i];
    for (int j=i+1; j<9; j++) { //searches for duplications
      if (y[j] ==  lineartemp)
	return 0;
	  }
  }
  return 1;
}

//Checks for duplications in each column
int ColumnCheck ( int x[9][9]) {
  for (int i=0; i<9; i++) {
    for (int j= 0; j<9; j++)
      temp[j] = x[j][i];

    if ( Check (temp) == 0 )
      return 0;
  }
  return 1;
}

//Checks for duplaication in all 9 subsquares
int SquaresCheck (int x[9][9]) {
  //column and row loops set the starting index for each subsquare.
  //ie (since I put column loop first),
  //[0][0], [3][0], [6][0], [0][3], [3][3], [6][3], [0][6],[3][6], [6][6]
  // i and j  are usual iterators to create the linear array,
  // and k iterates index of linear array (temp).

  int i;
  int j;
  int column;
  int row;
  int k;

  for (column=0; column <= 6; column += 3) {
    for (row=0; row <= 6; row += 3) {
      for (k=0, i=0; i<3; i++) {
	for (j=0; j<3; j++)
	  temp[k++] = x[row+i][column+j];
      }
      if (Check(temp) ==0)
	return 0;
    }
  }

  return 1;
}



int main()
{
     clrscr();
     cout <<"Enter 9 X 9 elements " << endl;
    for ( int i=0; i<9; i++)
    {
      for ( int j=0; j<9; j++)
	cin >> sudoku[i][j];
    }


  if ( RowCheck(sudoku) == 0 || ColumnCheck(sudoku)==0 || SquaresCheck(sudoku)==0)
   {
    cout<<"\nSudoku is incorrect\n";
    return 0;
   }

  cout<<"\nSudoku is correct\n";
  getch();
  return 0;
}

