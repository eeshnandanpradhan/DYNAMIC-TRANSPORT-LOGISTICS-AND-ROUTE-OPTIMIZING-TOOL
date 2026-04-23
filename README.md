#, distance)) 
self.graph[destination].append((source, distance)) 
graph_module.py 
class Graph: 
def  init (self): 
self.graph = {} 
def add_route(self, source, destination, distance): 
if source not in self.graph: 
self.graph[source] = [] 
if destination not in self.graph: 
self.graph[destination] = [] 
self.graph[source].append((destination 
def get_graph(self): 
return self.graph 
 
#route_optimizer.py 
import heapq 
class RouteOptimizer: 
def  init (self, graph): 
self.graph = graph 
def shortest_path(self, start, end): 
priority_queue = [(0, start, [])] 
visited = set() 
 
while priority_queue: 
cost, current, path = heapq.heappop(priority_queue) 
 
if current in visited: 
continue 
visited.add(current) 
path = path + [current] 
 
if current == end: 
return cost, path 
for neighbor, distance in self.graph[current]: 
if neighbor not in visited: 
heapq.heappush( 
priority_queue, 
(cost + distance, neighbor, path) 
)return float("inf"), [] 
#input_module.py 
def get_route_input(): 
routes = int(input("Enter number of routes: ")) 
route_list = [] 
for _ in range(routes): 
source = input("Enter source: ") 
destination = input("Enter destination: ") 
distance = int(input("Enter distance: ")) 
route_list.append((source, destination, distance)) 
start = input("Enter start location: ") 
end = input("Enter destination location: ") 
return route_list, start, end 
#output_module.py 
def display_output(distance, path): 
print("\n----- OPTIMIZED ROUTE ------ ") 
print("Best Route:", " -> ".join(path)) 
print("Minimum Distance:", distance, "km") 
#main.py 
from graph_module import Graph 
from route_optimizer import RouteOptimizer 
from input_module import get_route_input 
from output_module import display_output 
def main(): 
graph_obj = Graph() 
route_list, start, end = get_route_input() 
for source, destination, distance in route_list: 
graph_obj.add_route(source, destination, distance) 
optimizer = RouteOptimizer(graph_obj.get_graph()) 
distance, path = optimizer.shortest_path(start, end) 
display_output(distance, path) 
if  name == " main ": 
main()
