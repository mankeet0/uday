#include <stdio.h>
#include <stdlib.h>
#include<time.h>
int rollDie();
int player1 = 0, player2 = 0;
void printBoard()
{
   int board[101],alt = 0,LR = 101,RL = 80,val = 100,i;
   for ( i = 1; i <= 100; i++)
   {
   board[i] = i;
   }
   while (val--) {
   if (alt == 0) {
   LR--;
	    if (LR == player1) {
		printf("#P1\t");
	    }
	    else if (LR == player2) {
		printf("#P2\t");
	    }
	    else
		printf("%d\t", board[LR]);

	    if (LR % 10 == 1) {
		printf("\n");
		alt = 1;
		LR -= 10;
	    }
	}
	else {
	    RL++;
	    if (RL == player1) {
		printf("#P1\t");
	    }
	    else if (RL == player2) {
		printf("#P2\t");
	    }
	    else
		printf("%d\t", board[RL]);

	    if (RL % 10 == 0) {
		printf("\n");
		alt = 0;
		RL -= 30;
	    }
	}
	if (RL == 10)
	    break;
    }

    printf("\n");
}
int movePlayer(int currentPlayer, int roll)
{
    int i,newSquare,snakesAndLadders[101];
    int newPosition = currentPlayer + roll;
    for ( i = 0; i <= 100; i++)
    {
	snakesAndLadders[i] = 0;
    }
    snakesAndLadders[1] = 38;
    snakesAndLadders[4] = 11;
    snakesAndLadders[8] = 22;
    snakesAndLadders[21] = 21;
    snakesAndLadders[28] = 48;
    snakesAndLadders[50] = 17;
    snakesAndLadders[71] = 21;
    snakesAndLadders[32] = -22;
    snakesAndLadders[36] = -30;
    snakesAndLadders[48] = -22;
    snakesAndLadders[62] = -44;
    snakesAndLadders[88] = -64;
    snakesAndLadders[95] = -39;
    snakesAndLadders[97] = -19;
    newSquare= newPosition + snakesAndLadders[newPosition];
    if (newSquare > 100) {
	return currentPlayer;
    }
    return newSquare;
}

int main ()
{
    int currentPlayer = 1,won = 0,roll;
    srand(time(0));
    printf("Snake and Ladder Game\n");

    while (!won) {

	printf(
	    "\nPlayer %d, press Enter to roll the die...",
	    currentPlayer);
	getchar();
	roll = rollDie();
	printf("You rolled a %d.\n", roll);

	if (currentPlayer == 1) {
	    player1 = movePlayer(player1, roll);
	    printf("Player 1 is now at square %d.\n\n",
		   player1);
	    printBoard();
	    if (player1 == 100) {
		printf("Player 1 wins!\n");
		won = 1;
	    }
	}
	else {
	    player2 = movePlayer(player2, roll);
	    printf("Player 2 is now at square %d.\n\n",
		   player2);
	    printBoard();
	    if (player2 == 100) {
		printf("Player 2 wins!\n");
		won = 1;
	    }
	}


	currentPlayer = (currentPlayer == 1) ? 2 : 1;
    }

    return 0;
}
int rollDie()
{
return rand() % 6 + 1;
}
