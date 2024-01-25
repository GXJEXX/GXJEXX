import random

class LudoGame:
    def __init__(self, players):
        self.players = players
        self.board = [0] * 52  # Represents the Ludo board with 52 positions
        self.player_positions = {player: 0 for player in players}
        self.current_player = random.choice(players)

    def roll_dice(self):
        return random.randint(1, 6)

    def move_piece(self, player, steps):
        current_position = self.player_positions[player]
        new_position = (current_position + steps) % 52
        self.player_positions[player] = new_position

    def play_turn(self):
        steps = self.roll_dice()
        print(f"{self.current_player} rolled a {steps}")
        self.move_piece(self.current_player, steps)
        print(f"{self.current_player}'s position: {self.player_positions[self.current_player]}")

        # Check for special positions like snakes and ladders, or home
        # You can add your own rules here

        # Switch to the next player
        self.current_player = self.get_next_player()

    def get_next_player(self):
        current_index = self.players.index(self.current_player)
        next_index = (current_index + 1) % len(self.players)
        return self.players[next_index]

    def play_game(self):
        rounds = 10  # You can adjust the number of rounds
        for _ in range(rounds):
            self.play_turn()

if __name__ == "__main__":
    players = ["Player1", "Player2", "Player3", "Player4"]  # You can add more players
    game = LudoGame(players)
    game.play_game()

