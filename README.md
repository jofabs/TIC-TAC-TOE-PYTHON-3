# TIC-TAC-TOE-PYTHON-3
"""The classic tic-tac-toe game programmed in python with computer intelligence. Additional features include a two-player game mode, and saving and loading previous games."""
#This project was completed by Joseph A Fabiyi

# Address for my Blog https://aprogrammersdiary.wordpress.com/
# click the menu of the Blog home page to access blog pages and posts.
# About me page is just a short summary about myself.
# Coursework post links page consists of a list of the coursework post
# Blog posts page consists of all the posts themselves


#--------------------------------------------------------------------#

#tic tac toe game
import random #program for initiating random
import time #program for manipulating time
import pickle 
movesmade = []

def playerIdentity():
    """user choses who they want to play asand function returns what choose as string"""
      
    identity = ''
    while not (identity == 'X' or identity == 'O'):
        print('Do you want to be X or O?')
        identity = input().upper()

        if identity == 'X' or identity == 'x':#user can input x in either uppercase or lowercase
            print ("You have chosen to play as X.")
            return "x"
        elif identity == 'O' or identity == 'o':#user can input o in either uppercase or lowercase
            print("You have chosen to play as O.")
            return "o"

gameGrids = list(range(0,9))
#This is a list-range of numbers from which a function will draw its numbers from
def Savegame():
    global gameGrids
    f = open ("TTTGame.txt","wb")
    x = gameGrids
    pickle.dump(x,f)
    f.close()

def Loadgame():
    global gameGrids
    f = open ("TTTGame.txt", "rb")
    gameGrids = pickle.load(f)
    f.close()
     
def board() :
    """ This is a function for the board in which the tic tac toe game will be played """
    """ Also contains the spots in which the user can choose from to play """
    print ('|', gameGrids[0],'|' , gameGrids[1],'|' , gameGrids[2],'|')
    print ('|', '---------','|')
    print ('|', gameGrids[3],'|' , gameGrids[4],'|' , gameGrids[5],'|')
    print ('|', '---------','|')
    print ('|', gameGrids[6],'|' , gameGrids[7],'|' , gameGrids[8],'|')

def winner(gameGrids, gamer):
    """This function returns True if that player has won the game """
    """ or if the game ends in a tie """
     
    if (gameGrids [0] == gamer and gameGrids [1]== gamer and gameGrids [2] == gamer) or \
       (gameGrids [3] == gamer and gameGrids [4]== gamer and gameGrids [5] == gamer) or \
       (gameGrids [6] == gamer and gameGrids [7]== gamer and gameGrids [8] == gamer) or \
       (gameGrids [0] == gamer and gameGrids [3]== gamer and gameGrids [6] == gamer) or \
       (gameGrids [1] == gamer and gameGrids [4]== gamer and gameGrids [7] == gamer) or \
       (gameGrids [2] == gamer and gameGrids [5]== gamer and gameGrids [8] == gamer) or \
       (gameGrids [0] == gamer and gameGrids [4]== gamer and gameGrids [8] == gamer) or \
       (gameGrids [2] == gamer and gameGrids [4]== gamer and gameGrids [6] == gamer):
        return True
    
    else:
        return False
       
        
def boardWin():
    if winner(gameGrids, "x"):
        print()
        print ("X has won the game!")
        return "x"
    
    if winner(gameGrids, "o"):
        print()
        print ("O has won the game!")
        return "o"
    

    
#---------------- Start of Single Player --------------------#
def userChoice():
    """ This funtion is for the users input choice in the game"""
    """ the funtion also checks if the user input is valid and executes precaution if is not """
    while True:

            try:
                spot = input("please select a spot between 0 - 8")
                spot1 = int(spot)


                
                if (spot1 >= 0 and spot1 <= 8) and (gameGrids[spot1] != "x" and gameGrids[spot1] != "o"):
                    movesmade.append(spot)
                    return(spot1)
                elif spot1 == 99:
                    return(spot1)
                else:
                    spot = input("please select a spot between 0 - 8")
                    spot1 = int(spot)
                

            except ValueError:

                continue

            
def compChoice():
    """ This funtion is for the computers input choice in the game"""
    """ The computer inserts a random integer in a range of (0,8) into the game board"""

        #check how to win the game
    for i in range(0, 8):
        if gameGrids[i] == " ":
            gameGrids[i] == gamer
            makeMove(gameGrids, computerVar, i)
            if winner(gameGrids, computerVar):
                return i
            else:
                gameGrids[i] = " "

    #check how to defend 
    for i in range(0, 8):
        if gameGrids[i] == " ":
            gameGrids[i] == gamer
            if winner(gameGrids, gamer):
              makeMove(gameGrids, playerVar, i)
              if winner(gameGrids, playerVar):
                return i

    while True:
        spot2 = random.randint(0,8)
        if gameGrids[spot2] == "x" or gameGrids[spot2] == "o":
            pass
        else:
            movesmade.append(spot2)
            return spot2
        
def singlePlayerRun():
    """ This bit of code runs the single player game when called"""
    
    board()
 
    while len(movesmade)<=9:
        print()
        spot = userChoice()
        print()
        if spot == 99:
            Savegame()
            break
        gameGrids[spot] = playerVar
        board()
        winningAlp = boardWin()
    
        if winningAlp == "x":
            break

        elif winningAlp == "o":
            break
        
        elif len(movesmade)==9:
            print("TIE!")
            break
        
        print()
        print("The computer has made its move")
        print()
        spot2 = compChoice()
        gameGrids[spot2] = computerVar
        board()

        winningAlp = boardWin()
    
    
        if winningAlp == "x":
            break

        elif winningAlp == "o":
            break

#------------------END OF SINGLE PLAYER------------------#



#------------------ Start of MULTIPLAYER CODE ------------------#

def player1():
    """ This bit of code is for the first player in the multiplayer game"""
    #firstPlayer = player1()
    while True:

            try:
                spot = input("please select a spot between 0 - 8")
                spotPlayer1 = int(spot)


                
                if (spotPlayer1 >= 0 and spotPlayer1 <= 8) and (gameGrids[spotPlayer1] != "x" and gameGrids[spotPlayer1] != "o"):
                    movesmade.append(spot)
                    return(spotPlayer1)
                
                elif spotPlayer1 == 99:
                    return(spotPlayer1)
                
                else:
                    spot = input("please select a spot between 0 - 8")
                    spotPlayer1 = int(spot)
                

            except ValueError:

                continue

            
def player2():
    """ This bit of code is for the second player in the multiplayer game"""
    #secondPlayer = player2()
    while True:

            try:
                spot = input("please select a spot between 0 - 8")
                spotPlayer2 = int(spot)


                
                if (spotPlayer2 >= 0 and spotPlayer2 <= 8) and (gameGrids[spotPlayer2] != "x" and gameGrids[spotPlayer2] != "o"):
                    movesmade.append(spot)
                    return(spotPlayer2)
                
                elif spotPlayer2 == 99:
                    return(spotPlayer2)
                
                else:
                    spot = input("please select a spot between 0 - 8")
                    spotPlayer2 = int(spot)
                

            except ValueError:

                continue
            
def multiplayerRun():
    
    board()
    
    while len(movesmade)<=9:
        print()
        print("Please make a move Player 1")
        spotPlayer1 = player1()
        print()
        if spotPlayer1 == 99:
            Savegame()
            break
        gameGrids[spotPlayer1] = playerVar
        board()
        winningAlp = boardWin()
    
    
        if winningAlp == "x":
            break

        elif winningAlp == "o":
            break

        elif len(movesmade)==9:
            print("TIE!")
            break

        print()
        print("Please make a move Player 2")
        spotPlayer2 = player2()
        print()
        if spotPlayer2 == 99:
            Savegame()
            break
        gameGrids[spotPlayer2] = computerVar
        board()

        winningAlp = boardWin()
    
    
        if winningAlp == "x":
            break

        elif winningAlp == "o":
            break


#------------------ End of MULTIPLAYER CODE ------------------#





#------------------ Start of introduction ------------------#

print("Welcome to tic tac toe by Lord Alex")
print()
print("HELLO ! ")
print()
time.sleep(1/2) #next print half second delay

playerVar = playerIdentity()

if playerVar == "x":
    computerVar = "o"
else:
    computerVar = "x"

print()
print("INPUT : ")
print("'1' For Single player Mode.")#users option
print()
print("'2' For multiplayer Mode.") #users option
print()
print("'3' to run an existing SINGLE PLAYER Game.")
print()
print("'4' to run an existing MULTIPLAYER Game.")
print()
print("NOTE: TO SAVE THIS GAME AT ANY TIME PLEASE")
print("KEY IN NUMER (99) FOLLOWED BY THE ENTER KEY.")


while True:
    print()
    choice = input("Make a choice: ") #User makes a choice

    singleplayerMode= "1"
    
    multiplayerMode = "2"

    run = "3"

    start = "4"

    
    if choice == singleplayerMode:
        print()
        print("You have selected Single player Mode.")
        print()
        #this is where i will type all the code for single player mode
        singlePlayerRun()
        break
    elif choice == multiplayerMode:
        print()
        print("You have selected Multiplayer Mode.")
        print()
        #this is where you type in all the code for multiplayer mode
        multiplayerRun()
        break
    elif choice == run:
        print()
        print("You are returning to a saved game...")
        print()
        Loadgame()
        singlePlayerRun()
        break
    elif choice == start:
        print()
        print("You are returning to a saved game...")
        print()
        Loadgame()
        multiplayerRun()
        break

#conditions if user choses wrong
    print ("You have entered an invalid choice !")
    print ("Please try again..")


#------------------ End of introduction ------------------#
