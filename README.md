from collections import deque

def shortest_connection(graph, start, target):
    queue = deque([[start]])
    visited = set([start])

    while queue:
        path = queue.popleft()
        person = path[-1]

        if person == target:
            return path

        for friend in graph.get(person, []):
            if friend not in visited:
                visited.add(friend)
                queue.append(path + [friend])

    return None


# Example social network
graph = {
    "Alice": ["Bob", "Charlie"],
    "Bob": ["Alice", "David"],
    "Charlie": ["Alice", "Emma"],
    "David": ["Bob", "Emma", "Frank"],
    "Emma": ["Charlie", "David"],
    "Frank": ["David"]
}

start = "Alice"
target = "Frank"

connection = shortest_connection(graph, start, target)

if connection:
    print("Shortest connection:")
    print(" -> ".join(connection))
    print("Number of connections:", len(connection) - 1)
else:
    print("No connection found.")
