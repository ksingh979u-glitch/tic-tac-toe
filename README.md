#include <iostream>
#include <cctype>   

using namespace std;

void board(char array[][3])
{
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            cout << "  " << array[i][j] << "  ";
            if (j < 2)
            {
                cout << "|";
            }
        }
        cout << endl;

        if (i < 2)
        {
            cout << "_____|_____|_____";
        }
        cout << endl;
    }
}

int main()
{
    char choice;
    int row, colum;

    char array[3][3] = {
        {' ', ' ', ' '},
        {' ', ' ', ' '},
        {' ', ' ', ' '}};

    cout << "Player 1 choose (X/O): ";
    cin >> choice;
    choice = toupper(choice);

    if (choice != 'X' && choice != 'O')
    {
        cout << "Wrong choice\n";
        return 0;
    }

    for (int move = 0; move < 9; move++)
    {
        board(array);

        cout << "Enter row and column (0-2): ";
        cin >> row >> colum;

        if (row < 0 || row > 2 || colum < 0 || colum > 2)
        {
            cout << "Wrong input\n";
            move--; // retry same turn
            continue;
        }

        if (array[row][colum] != ' ')
        {
            cout << "Place already filled\n";
            move--; 
            continue;
        }

        array[row][colum] = choice;

        
        for (int k = 0; k < 3; k++)
        {
            if (array[k][0] == choice && array[k][1] == choice && array[k][2] == choice)
            {
                board(array);
                cout << choice << " WON\n";
                return 0;
            }
        }

        
        for (int k = 0; k < 3; k++)
        {
            if (array[0][k] == choice && array[1][k] == choice && array[2][k] == choice)
            {
                board(array);
                cout << choice << " WON\n";
                return 0;
            }
        }

      
        if (array[0][0] == choice && array[1][1] == choice && array[2][2] == choice)
        {
            board(array);
            cout << choice << " WON\n";
            return 0;
        }

        if (array[0][2] == choice && array[1][1] == choice && array[2][0] == choice)
        {
            board(array);
            cout << choice << " WON\n";
            return 0;
        }

        
        if (choice == 'X')
        {
            choice = 'O';
        }
        else
        {
            choice = 'X';
        }
    }

    
    board(array);
    cout << "It's a DRAW\n";

    return 0;
}
