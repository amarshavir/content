+++
title = "Pythonic activies - tik tac toe"
tags = ["development" , "python"]
date = "2022-12-22"
author = "Robel Schwarz"
+++

## A while ago
during my first year of comp sci, I was tasked to create a game of tik tac toe. While not a complex procedure, I decided to make it more complicated for myself. In challenging my younger self, I went through 3 development phases.

### The base game
I do not have the files for the base game; if I find the Replit file, I will make sure to fill this section of the story. Until then, my dear reader, you can use your wonderful imagination.


### Adding "Features."
the more complicated procedure that I eluded to before was adding variable board sizing. This dynamic board sizing was an exercise in mental gymnastics.

The game was initialized using a relatively simple setup. Definition vars as needed and whatnot. The worst thing about my original code was my gosh darn global vars. Do not use or make anything like this. I want to cry reading back at my old code.


    def main():
    import os
    global b
    def cls():
        os.system('cls' if os.name=='nt' else 'clear')

    b = int(input("how big do you want the board: "))

    col_sto = []
    ls_turn = []
    players = ['x','o']
    board = []
    turn_count = 0
    for x in range(0, b):
        for x in range(0, b):
            board.append("-")
    game_active = True
    while game_active == True:
        test = int(input(":")) - 1
        ls_turn.append(test)
        while len(ls_turn) != len(set(ls_turn)):
            ls_turn = list(dict.fromkeys(ls_turn))
            test = int(input(" :"))-1
            ls_turn.append(test)
        board[test] = players[0]

        global ls
        ls = [board[x:x + b] for x in range(0, len(board), b)]
        test_ls = [board[x:x + b] for x in range(0, len(board), b)]

        def display():
            for i in ls:
                print(i)
        cls()
        display()

        def end_game():
            global game_active
            wld = input("would you like to play again[y/n]: ")
            if wld == "y":
            main()
            else: 
            quit()

        def row_allcheck():
            global winner
            for x in range(0, b):

                if all(x == ls[0][0] for x in ls[0]):
                    #print("All elements in list are equal")
                    winner = ls[0][0]
                    if winner == '-':
                        None
                    if winner == 'x' or 'o':
                        return winner
                    
                #else:
                #print("All elements in list are not equal")
                del ls[0]
            #print(winner)

        def col_allcheck():
            global winner
            global col_sto
            col_sto = []
            ls = [board[x:x+b] for x in range(0, len(board),b)]
            global loop1
            global loop2
            loop1 = 0
            loop2 = 0
            #col
        
            def  col_check(loop1):
                for x in range(0,b):
                del ls[0+loop1][1:b]
                if loop1 < b-1:
                loop1 = loop1 +1
        
                return(ls)
            def col_rotate(loop2):
            global winner
            for x in range(0,b):
            del ls[loop2][0]
            loop2 = loop2 + 1
            return(ls)

            colcheck = []
            col = 0
            for x in range(0,b):

            for x in range(0,col):
            ls = col_rotate(loop2)
            
        

        
            colcheck = [tuple(lst) for lst in ls]
            
            if(len(set(colcheck))==1):
            #print("col_All elements in list are the same")
            winner = colcheck[0][0]
            if winner == '-':
                None

            
            if winner == 'o' or 'x':
                return winner
            #else:
                #print("col_All elements in list are not same")
            
        
            ls = [board[x:x+b] for x in range(0, len(board),b)]
            if col < b:
                col = col + 1

        def dia_allcheck():
            global winner
            ls = [board[x:x + b] for x in range(0, len(board), b)]
            #dia check 1
            #print("dia")
            dia = 0
            dia1 = []
            for x in range(0, b):
                dia1.append(ls[dia][dia])
                if dia < b:
                    dia = dia + 1
            #print(dia1)
            if (len(set(dia1)) == 1):
                #print("All elements in list are same")
                winner = dia1[0]
                if winner == '-':
                    None
                if winner == 'o' or 'x':
                    return winner
                
                #print(winner)
            #else:
            #print("All elements in list are not same")

            ls = [board[x:x + b] for x in range(0, len(board), b)]
            #dia check 2
            #print("dia2")
            dia2 = []
            dia = 0
            for x in range(0, b):
                dia2.append(ls[dia][b - dia - 1])
                if dia < b:
                    dia = dia + 1
            #print(dia2)
            if (len(set(dia2)) == 1):
                #print("All elements in list are same")
                winner = dia2[0]
                #print(winner)
            #else:
            #print("All elements in list are not same")

        row_allcheck()
        col_allcheck()
        dia_allcheck()
        players.reverse()
        if winner == 'o' or winner == 'x':
            print(winner + " wins the game")
            end_game()

        turn_count = turn_count + 1
        if turn_count == b*b:
            if winner != 'x' and winner != 'o':
            print("looks like a tie")
            end_game()

    main()    


The single most important line to make the dynamic board sizing is

    ls = [board[x:x + b] for x in range(0, len(board), b)]

This line iterates over the index to create a hashmap. I will not lie. I totally copy pasted this line from StackOverflow from 3 years ago. Oddly enough, it was the only line I copied, but it also happened to be the most significant.


### Optmization

I wrote the original code for my class in April 2020, but later that year, I had a day of free time in October, which I proceeded to spend on pointless activities. I wanted to update my code base. Funny enough, my old code was so bad it was easier for me to create an entirely new program from start to finish.


    import os
    def cls():
        os.system('cls' if os.name=="nt" else 'clear')

    class Main:
        def __init__(self , input_size):
            self.active = True
            self.players = ['x' , 'o']
            self.board = []
            self.divided_board_array = None
            self.size = input_size 
        def init_board(self):
            for x in range(0 , (self.size) ** 2):
                self.board.append("-")
        
        def display(self): 
            self.divided_board_array = [self.board[x:x + self.size] for x in range(0, (self.size) **2, self.size)]
            for i in self.divided_board_array:
                print(i)
        
        def player_turn(self):
            turn = int(input(": ")) - 1
            if (self.board[turn] =="-"): 
                self.board[turn] = self.players[0]
            else:
                cls()
                self.display()
                print("that space is already taken, player: (" + self.players[0] + ") pick a different space")
                self.player_turn()
        
        def col_check(self):
            for j in range(0 , self.size):
                row = []
                for i in self.divided_board_array:
                    row.append(i[j])
                if(len(set(row))==1):
                    if (row[0] == "-"):
                        return False
                    else:
                        return True
                else:
                    return False
        def row_check(self):
            for i in self.divided_board_array:
                if(len(set(i))==1):
                    if (i[0] == "-"):
                        return False
                    else:
                        return True
                else:
                    return False
        def dia_check(self):
            def check_fn(index , tf):
                ls = []
                for i in range(0 , self.size):
                    ls.append(self.board[index])
                    if (tf):
                        index += self.size +1
                    else:
                        index += self.size -1
                if (len(set(ls)) == 1):
                    if(ls[0] == "-"):
                        return	False
                    else:
                        return True
                else:
                    return False

            if(check_fn(self.size - 1 , False) or check_fn(0 , True)):
                return True
            else:
                return False
            
    inp = int(input("How big do you want the board?: "))
    game = Main(inp)

    game.init_board()
    cls()
    game.display()
    while game.active:
        game.player_turn()
        cls()
        game.display()
        if (game.dia_check() or game.col_check() or game.row_check()):
            game.active = False
            print("winner : " + game.players[0])
        game.players.reverse()


I completed my goal of making the game with cleaner, more "pythonic" code. I removed all of the global vars and had a great time spamming for j and i loops.
You might have noticed I carried over my magical board rendering method.



    [self.board[x:x + self.size] for x in range(0, (self.size) **2, self.size)]


Since the line was never hard coded on any set values. Building the new source code with this line as the base was a relatively easy task.

## What I learned


Is some times, it's better to cut your losses and start over. While this is not the first nor the last time I spent a lot of time on a pointless task, it is good to look at a relatively harmless example of stupidity and learn from it. At some point, you will get better, it will be a long and hard road, but you will make it.


<3

blessings,
Isayas