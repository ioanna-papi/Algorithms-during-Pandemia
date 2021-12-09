from collections import deque
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("num_nodes", type=int, help="number of nodes")
parser.add_argument("input_file",help="name of input file")
parser.add_argument("-c", "--connections", action="store_true")
parser.add_argument("-r", "--radius", type=int, help="the ball's radius")
args = parser.parse_args()

g = {}
degree = {}
influence = {}
key = []
with open(args.input_file) as graph_input:
    for l in graph_input:
        nodes = [int(x) for x in l.split()]
        if (len(nodes) != 2):
            continue
        if (nodes[0] not in g):
            g[nodes[0]] = []
        if (nodes[1] not in g):
            g[nodes[1]] = []
        g[nodes[0]].append(nodes[1])
        g[nodes[1]].append(nodes[0])

for k in g.keys():
    key.append(k)

for k1 in key:
    degree[k1] = 0
    for k2 in key:
        if (k2 in g[k1]):
            degree[k1] += 1

def quarantine(g):
    h1 = list(g. keys())
    h1.sort()
    h2 = list(g.values())
    max1 = max(h2)
    for k in h1:
        if (g[k] == max1):
            return k

def distance(g, node):
    q = deque()
    q.appendleft(node)
    level = {node: 0}
    while (len(q) != 0):
        c = q.pop()
        for v in g[c]:
            if v not in level :
                q.appendleft(v)
                level[v] = level[c] + 1
    return level

# first algorithm
if (args.connections):
    for i in range(0, args.num_nodes):
        e = quarantine(degree)
        print(e, degree[e])
        for k in degree.keys():
            if (e in g[k]):
                degree[k] -= 1
        del degree[e]


def changeInfluence(k,degree):
    inf = 0
    sum = 0
    lev = distance(g, k)
    for l in lev:
        if (lev[l] == args.radius):
            sum += (degree[l] - 1)
    inf = (degree[k] - 1) * sum
    return inf



# second algorithm
if (args.radius):
    r = args.radius
    for i in key:
        sum = 0
        influence[i] = 0
        lev = distance(g,i)
        for l in key:
            if (lev[l] == r):
                sum += (degree[l] - 1)
        influence[i] = (degree[i] - 1) * sum

    for i in range(0, args.num_nodes):
        e = quarantine(influence)
        print(e, influence[e])
        for k in degree.keys():
            if (e in g[k]):
                g[k].remove(e)
                degree[k] -= 1
        del degree[e]
        del influence[e]
        lev2 = distance(g,e)
        for i in influence.keys():
            if (i in lev2 and lev2[i] <= (r + 1)):
                influence[i] = changeInfluence(i,degree)
