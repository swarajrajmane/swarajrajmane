#include <stdio.h>

#include <stdlib.h>

#include <windows.h>

#include <time.h>

#define WIDTH 30

#define HEIGHT 20

int x, y, fruitX, fruitY, score;

int tailX[100], tailY[100];

int nTail;

int gameOver;

enum Direction { STOP = 0, LEFT, RIGHT, UP, DOWN };

enum Direction dir;

void Setup() {

gameOver = 0;

dir = STOP;

x = WIDTH / 2;

y = HEIGHT / 2;

fruitX = rand() % WIDTH;

fruitY = rand() % HEIGHT;

score = 0;

}

void Draw() {

system("cls");

for (int i = 0; i < WIDTH + 2; i++) printf("#");

printf("\n");



for (int i = 0; i < HEIGHT; i++) {

    for (int j = 0; j < WIDTH; j++) {

        if (j == 0) printf("#");



        if (i == y && j == x)

            printf("O");

        else if (i == fruitY && j == fruitX)

            printf("F");

        else {

            int printTail = 0;

            for (int k = 0; k < nTail; k++) {

                if (tailX[k] == j && tailY[k] == i) {

                    printf("o");

                    printTail = 1;

                }

            }

            if (!printTail) printf(" ");

        }



        if (j == WIDTH - 1) printf("#");

    }

    printf("\n");

}



for (int i = 0; i < WIDTH + 2; i++) printf("#");

printf("\n");



printf("Score: %d\n", score);

printf("Controls: W=Up, A=Left, S=Down, D=Right, X=Exit\n");

}

void Input() {

if (GetAsyncKeyState('A') & 0x8000) dir = LEFT;

if (GetAsyncKeyState('D') & 0x8000) dir = RIGHT;

if (GetAsyncKeyState('W') & 0x8000) dir = UP;

if (GetAsyncKeyState('S') & 0x8000) dir = DOWN;

if (GetAsyncKeyState('X') & 0x8000) gameOver = 1;

}

void Logic() {

int prevX = tailX[0];

int prevY = tailY[0];

int prev2X, prev2Y;



tailX[0] = x;

tailY[0] = y;



for (int i = 1; i < nTail; i++) {

    prev2X = tailX[i];

    prev2Y = tailY[i];

    tailX[i] = prevX;

    tailY[i] = prevY;

    prevX = prev2X;

    prevY = prev2Y;

}



switch (dir) {

    case LEFT: x--; break;

    case RIGHT: x++; break;

    case UP: y--; break;

    case DOWN: y++; break;

    default: break;

}



if (x < 0 || x >= WIDTH || y < 0 || y >= HEIGHT)

    gameOver = 1;



for (int i = 0; i < nTail; i++) {

    if (tailX[i] == x && tailY[i] == y)

        gameOver = 1;

}



if (x == fruitX && y == fruitY) {

    score += 10;

    fruitX = rand() % WIDTH;

    fruitY = rand() % HEIGHT;

    nTail++;

}

}

int main() {

srand(time(0));

Setup();

while (!gameOver) {

    Draw();

    Input();

    Logic();

    Sleep(100);

}



system("cls");

printf("Game Over!\nYour final score: %d\n", score);

return 0;

}
