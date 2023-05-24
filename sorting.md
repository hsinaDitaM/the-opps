# PLAN
1. Data Structure: Define a data structure to store NBA statistics. For example, you can create a class called PlayerStats with attributes like name, points, rebounds, assists, etc. You can also create a list to store instances of the PlayerStats class.
 
 ```python
class PlayerStats:
    def __init__(self, name, points, rebounds, assists):
        self.name = name
        self.points = points
        self.rebounds = rebounds
        self.assists = assists

# Example list of player statistics
player_stats_list = [
    PlayerStats("LeBron James", 27.4, 8.5, 7.4),
    PlayerStats("Stephen Curry", 30.1, 5.5, 6.2),
    PlayerStats("Kevin Durant", 29.3, 7.1, 5.6),
    PlayerStats("Giannis Antetokounmpo", 28.1, 11.0, 6.1),
    # Add more player stats...
]

def sort_stats_by_attribute(stats_list, attribute):
    return sorted(stats_list, key=lambda x: getattr(x, attribute))

# Example usage to sort player stats by points
sorted_stats = sort_stats_by_attribute(player_stats_list, 'points')

def print_stats(stats_list):
    for player in stats_list:
        print(f"Player: {player.name}\tPoints: {player.points}\tRebounds: {player.rebounds}\tAssists: {player.assists}")

# Example usage to print sorted player stats
print_stats(sorted_stats)


