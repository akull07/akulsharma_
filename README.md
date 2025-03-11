import heapq

class Node:
    def __init__(self, position, g=0, h=0, parent=None):
        self.position = position
        self.g = g  # Cost from start node
        self.h = h  # Heuristic (estimated cost to goal)
        self.f = g + h  # Total cost (f = g + h)
        self.parent = parent

    def __lt__(self, other):
        return self.f < other.f


def a_star(start, goal, grid):
    # Define the possible movements (left, right, up, down)
    neighbors_offset = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    
    def heuristic(a, b):
        # Manhattan distance
        return abs(a[0] - b[0]) + abs(a[1] - b[1])

    def get_neighbors(node):
        neighbors = []
        for offset in neighbors_offset:
            neighbor_pos = (node.position[0] + offset[0], node.position[1] + offset[1])
            if 0 <= neighbor_pos[0] < len(grid) and 0 <= neighbor_pos[1] < len(grid[0]) and grid[neighbor_pos[0]][neighbor_pos[1]] == 0:
                neighbors.append(neighbor_pos)
        return neighbors

    open_list = []
    closed_list = set()
    
    start_node = Node(start, 0, heuristic(start, goal))
    heapq.heappush(open_list, start_node)
    
    g_scores = {start: 0}
    came_from = {}

    while open_list:
        current_node = heapq.heappop(open_list)
        
        if current_node.position == goal:
            # Reconstruct the path
            path = []
            while current_node:
                path.append(current_node.position)
                current_node = current_node.parent
            return path[::-1]  # Return the path from start to goal
        
        closed_list.add(current_node.position)

        for neighbor_pos in get_neighbors(current_node):
            if neighbor_pos in closed_list:
                continue

            g_score = current_node.g + 1  # Each move has a cost of 1
            if neighbor_pos not in g_scores or g_score < g_scores[neighbor_pos]:
                g_scores[neighbor_pos] = g_score
                h_score = heuristic(neighbor_pos, goal)
                neighbor_node = Node(neighbor_pos, g_score, h_score, current_node)
                heapq.heappush(open_list, neighbor_node)

    return None  # Return None if no path is found

# Example grid (0 = walkable, 1 = obstacle)
grid = [
    [0, 0, 0, 0, 0],
    [0, 1, 1, 1, 0],
    [0, 0, 0, 1, 0],
    [0, 1, 0, 0, 0],
    [0, 0, 0, 1, 0]
]

start = (0, 0)
goal = (4, 4)

path = a_star(start, goal, grid)
print("Path:", path)
 


