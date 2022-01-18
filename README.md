# Problem description (in greek)
In the Description.pdf

Alternatively, visit: https://nbviewer.jupyter.org/github/dmst-algorithms-course/assignment-2020-2/blob/master/assignment_2020_2.ipynb?flush_cache=true

# How to run the code:
    python network_destruction.py [-c] [-r RADIUS] num_nodes input_file

Depending on your computer's operating system you may need to provide python3 or something instead of python.

The brackets are not part of the things given by the user, they just serve to remind us in the program description that this parameter is optional. So we have:

If the -c parameter is given, the program will use the number of links of each node and not the total influence. That is, it will work like the first example we gave. Otherwise, the program will use the overall influence, ie it will work like the second example.

If the parameter -r RADIUS is given the program will use the RADIUS value for r.

The num_nodes parameter corresponds to the number of nodes we want to remove.

The input_file parameter is the name of the file that describes the graph. 

You can use as an input file, one of those I have uploaded in the repository.
