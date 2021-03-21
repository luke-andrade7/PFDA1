#include <iostream>
#include <string>
#include <ctime>
#include <cstdlib> //to use NULL and clear the screen

using namespace std;

/*********************************************************************
** Function: get_puzzle
** Description: gets puzzle
** Parameters: sentence
** Pre-Conditions: sentence was declared in main
** Post-Conditions: saves sentence
*********************************************************************/
//get message
void get_puzzle (string& sentence){ //giving a copy name
	cout << "Enter a secret puzzle: " << endl;
	getline(cin, sentence);
	system("clear"); //clears the screen
}
/*********************************************************************
** Function: get_user_inputs
** Description: prompts for num of rounds and players
** Parameters: rounds, players
** Pre-Conditions: rounds and players declared in main
** Post-Conditions: valid ints
*********************************************************************/
int get_user_inputs(int& rounds, int& players){
	//int rounds, players;
	cout << "Welcome to Wheel of Fortune!" << endl;
	cout << "How many rounds would you like to play? ";
	cin >> rounds;
	
	cout << "How many players will be playing(max of 3 players)? ";
	cin >> players;
	cin.ignore();
}
/*********************************************************************
** Function: hidden_puzzle
** Description: hides puzzle with dashes and outputs it
** Parameters: hidden, str
** Pre-Conditions: puzzle had had a value and hidden declared in main
** Post-Conditions: sets hidden to hidden puzzle
*********************************************************************/
void hidden_puzzle (string& hidden, string str){
	int i;
	hidden.clear();
	for (i=0; i != str.length(); i++){
		if(str.at(i) >= 97 || str.at(i)>= 122){
            hidden += '-';
        }
        else if(str.at(i) >= 65 || str.at(i)>= 90){
            hidden += '-';
        }
        else if(str.at(i) = 32){
            hidden += ' ';
        }
	}
	cout << "Your puzzle is: " << hidden << endl;
}
/*********************************************************************
** Function: spin
** Description: gets a random number from 0 to 21
** Parameters: num
** Pre-Conditions: gets pre defined num from main
** Post-Conditions: return num
*********************************************************************/
int spin(int& num){
	srand(time(NULL));
	num = rand()%22;
	return num;
}
/*********************************************************************
** Function: complete_puzzle
** Description: checks to see if guess of puzzle is correct
** Parameters: puzzle, roundover
** Pre-Conditions:puzzle has been defined
** Post-Conditions: returns true or false depending on right or wrong
*********************************************************************/
bool complete_puzzle (string puzzle, bool& roundover){
	string guess;
	cout << "Enter your guess: ";
		getline (cin, guess);
	//make function to set money if correct or not.
	if (guess == puzzle){
		cout << "You guessed it correct! You now get everyone elses money and set them to 0." << endl;
		roundover = true;
		
		//keeps money from the round
		//everyone else loses their money for that round
	}
	else if (guess != puzzle){
		cout << "Thats wrong! You lose your turn to next player." << endl;
		roundover = true;
	}
}
/*********************************************************************
** Function: game_winner
** Description: compares game totals for who has the most money
** Parameters: total1, total2, total3
** Pre-Conditions: pre defined ints in main with values
** Post-Conditions: none
*********************************************************************/
void game_winner (int& total1, int& total2, int& total3){
	if ((total1 > total2) && (total1 > total3)){
		cout << "Player 1 wins the game with the most money: " << total1 << endl;
	}
	else if ((total2 > total1) && (total2 > total3)){
		cout << "Player 2 wins the game with the most money: " << total2 << endl;
	}
	else if ((total3 > total1) && (total3 > total2)){
		cout << "Player 3 wins the game with the most money: " << total3 << endl;
	}
}
/*********************************************************************
** Function: update_sec_mess
** Description: updates the hidden message
** Parameters: hidden, str, letter
** Pre-Conditions: strings predefined, letter inputed
** Post-Conditions: hidden is changed
*********************************************************************/
void update_sec_mess(string& hidden, string& str, char& letter){
    for(int i=0; i < str.length(); i++)
    {
        if(str.at(i) == letter)
        {
          hidden.at(i) = letter;
        }
    }
    cout << "The message is: " << hidden << endl;
}
/*********************************************************************
** Function: get_letter
** Description: prompts to set letter to a char
** Parameters: letter
** Pre-Conditions: letter declared in main 
** Post-Conditions: letter updated with this value
*********************************************************************/
void get_letter(char &letter){
    cout << "Guess a letter: ";
    cin >> letter;
    cin.ignore();
}
/*********************************************************************
** Function: letters_found_to_add_money
** Description: checks how many letters were found and does the calculation to update total money
** Parameters: str, letter, num, roundover, playerTotal
** Pre-Conditions: strings and valued declared elsewhere
** Post-Conditions: updates money, if round is over and gives number of values found
*********************************************************************/
void letters_found_to_add_money (string str, char& letter, int num, bool& roundover, int& playerTotal){
    int found = 0;
	for(int i=0; i < str.length(); i++){
        if(str.at(i) == letter){
           found = found + 1;
        }
    }
    playerTotal = num * found;
    cout << found << " found. Total: $" << playerTotal << endl;
    if(found == 0){
		cout << "You guessed incorectly:(" << endl;
        roundover = true;
    }
}
/*********************************************************************
** Function: check_wheel
** Description: checks random number received from rand generator
** Parameters: num, playertotal, puzzle, hddenPuzzle, letter, roundover
** Pre-Conditions: strings and values taken from address in main
** Post-Conditions: changes roundover, total money, updates puzzle and calls letters found money functions
*********************************************************************/
void check_wheel(int num, int& playertotal, string puzzle, string& hiddenPuzzle, char& letter, bool& roundover){
	//int num;
	if (num == 0){
		cout << "You got " << num << " so you have gone bankrupt!" << endl;
		playertotal = 0;
		roundover = true;
	}
	else if (num == 21){
		cout << "You got 21 so you lose a turn, but keep your money." << endl;
		roundover = true;
		//add money earned to their total
	}
	else if ((num > 0) && (num <21)){
		cout << "You landed on " << num << ", a number that is between 0 and 21, guess a vowel letter!" << endl;
		roundover = false;
		get_letter(letter);
		update_sec_mess(hiddenPuzzle, puzzle, letter); //updates hidden with letter 
		letters_found_to_add_money (puzzle, letter, num, roundover, playertotal); //checks for letter to add money
	}
}
/*********************************************************************
** Function: can_buy_a_vowel
** Description: checks if player has enough money to buy a vowel - removes 10 dollars if do
** Parameters: playertotal, puzzle, hiddenPuzzle, letter
** Pre-Conditions: variables/ strings declared and borrowed from main
** Post-Conditions: are allowed to buy a vowel
*********************************************************************/
void can_buy_a_vowel (int& playertotal, string puzzle, string& hiddenPuzzle, char& letter){
	if (playertotal >= 10){
		playertotal = playertotal-10;
		get_letter(letter);
		update_sec_mess(hiddenPuzzle, puzzle, letter); //updates hidden with letter
	}else cout << "You do not have enough money!:(" << endl; 
}
/*********************************************************************
** Function: print_menu
** Description: prints main menu with questions
** Parameters: puzzle, hiddenPuzzle, letter, playertotal, num, roundover
** Pre-Conditions: strings and variables defined in main choose a number between 1 and 3
** Post-Conditions: prints out the choice
*********************************************************************/
void print_menu(string& puzzle, string& hiddenPuzzle, char& letter, int& playertotal, int& num, bool& roundover){
	int answer;
	bool win;
	cout << "Would you like to: " << endl; 
	cout << "   (1)Spin the wheel " << endl;
	cout << "   (2)Solve the puzzle " << endl;
	cout << "   (3)Buy a vowel" << endl;
	cin >> answer;
	cin.ignore();
	
	//could make these to functions
	if (answer == 1){
		spin(num); //spin wheel to get rand num
		check_wheel(num, playertotal, puzzle, hiddenPuzzle, letter, roundover);
		
	}
	else if (answer == 2){
		complete_puzzle (puzzle, roundover);
		//function checking if won the game (guessed correct) then keep everyones money and they go bankrupt
		}
	else if (answer == 3){
		can_buy_a_vowel (playertotal, puzzle, hiddenPuzzle, letter);//can keep adding letters
	}
}
/*********************************************************************
** Function: main
** Description: runs the program with all the functions
** Parameters: none
** Pre-Conditions: none
** Post-Conditions: none
*********************************************************************/
int main(){
//variables:
	int num = 0, rounds, players, roundTotal1=0, roundTotal2=0, roundTotal3=0, total1=0, total2=0, total3=0, found; //need something to set spin to a value
	string puzzle, hiddenPuzzle; //variable where puzzle will be set
	char vowel;
	bool roundover = false, gameover = false;
	
	//Gets the puzzle and the rounds and players playing
		get_user_inputs(rounds, players);

	//need to loop until player loses turn
	switch(players){
	case 1:
		for(int i=1; i<=rounds; i++){ //looping for amount of rounds specified
			
			get_puzzle (puzzle); //gets puzzle string
		//Hides puzzle	
			hidden_puzzle (hiddenPuzzle, puzzle);  //changing hidden puzzle into dashes
			
			do{
		//Pints the menu for player
			print_menu(puzzle, hiddenPuzzle, vowel, total1, num, roundover);
		
			}while (roundover != true); //loop while someone hasnt won
		}
		//Compare game totals to see who has won
			game_winner (total1, total2, total3);
		break;
		
	}
	/*case 2:
		for(int i=1; i<=rounds;i++){
			get_puzzle (puzzle); //gets puzzle string
		}
	break;
	case 3:
		for(int i=1; i<=rounds;i++){
			get_puzzle (puzzle); //gets puzzle string
		}
	break;
	} */
	return 0;
}
