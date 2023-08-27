import random

"""This program plays a game of Rock, Paper, Scissors between two Players,
and reports both Player's scores each round."""

moves = ['rock', 'paper', 'scissors']

"""The Player class is the parent class for all of the Players
in this game"""


class Player:
    def move(self):
        return 'rock'

    def learn(self, my_move, their_move):
        pass


# need to create the RandomPlayer subclass
class RandomPlayer(Player):
    def move(self):
        return random.choice(moves)


# need to create the HumanPlayer subclass
class HumanPlayer(Player):
    def move(self):
        move = ''
        while move not in moves:
            move = input("Rock, Paper, or Scissors? ").lower()
            if move not in moves:
                print("Invalid move. Please enter Rock, Paper, or Scissors.")
        return move


class ReflectPlayer(Player):
    def __init__(self):
        self.last_opponent_move = random.choice(moves)

    def move(self):
        return self.last_opponent_move

    def learn(self, my_move, their_move):
        self.last_opponent_move = their_move


class CyclePlayer(Player):
    def __init__(self):
        self.next_move = random.choice(moves)

    def move(self):
        current_move = self.next_move
        if current_move == 'rock':
            self.next_move = 'paper'
        elif current_move == 'paper':
            self.next_move = 'scissors'
        else:
            self.next_move = 'rock'
        return current_move

    def learn(self, my_move, their_move):
        pass  # don't need this bc moves are pre-determined.


def beats(one, two):
    return ((one == 'rock' and two == 'scissors') or
            (one == 'scissors' and two == 'paper') or
            (one == 'paper' and two == 'rock'))


class Game:
    def __init__(self, p1, p2):
        self.p1 = p1
        self.p2 = p2
        self.p1_score = 0
        self.p2_score = 0

    def play_round(self):
        move1 = self.p1.move()
        move2 = self.p2.move()
        print(f"Player 1: {move1}  Player 2: {move2}")
        if beats(move1, move2):
            self.p1_score += 1
            print("Player 1 wins this round!")
        elif beats(move2, move1):
            self.p2_score += 1
            print("Player 2 wins this round!")
        else:
            print("It's a tie!")
        # self.p1.learn(move1, move2)
        # self.p2.learn(move2, move1)

    def play_game(self):
        print("Game start!")
        round_num = 1
        while True:
            print(f"Round {round_num}:")
            self.play_round()

            # is a player ahead by two points (and at least 2 rounds played)
            if round_num > 1 and abs(self.p1_score - self.p2_score) >= 2:
                break

            # does user want to continue or quit
            continue_game = input("Type 'quit' to end the game or"
                                  " press Enter to continue: ").lower()

            while continue_game not in ['quit', '']:
                print("Invalid input. Please type 'quit' or press Enter.")
                continue_game = input("Type 'quit' to end the game"
                                      " or press Enter to continue: ").lower()

            if continue_game == 'quit':
                break

            round_num += 1

        print(f"Final Score: Player 1: {self.p1_score},"
              f" Player 2: {self.p2_score}")
        if self.p1_score > self.p2_score:
            print("Player 1 wins the game!")
        elif self.p2_score > self.p1_score:
            print("Player 2 wins the game!")
        else:
            print("The game is a tie!")
        print("Game over!")


if __name__ == '__main__':
    print("Playing against ReflectPlayer:")
    game = Game(HumanPlayer(), ReflectPlayer())
    game.play_game()

    play_next = input("Would you like to play against"
                      " the CyclePlayer? (yes/no): ").lower()
    if play_next == 'yes':
        print("\nPlaying against CyclePlayer:")
        game = Game(HumanPlayer(), CyclePlayer())
        game.play_game()
    else:
        print("Thanks for playing!")
