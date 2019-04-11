# gitLab
lab 10 cs210
"""
Program: CS 115 Lab 4d
Author: oren gremberg
Description:This program draws a line graph.This program draws a graph and determines whether
   consecutive points are increasing or decreasing. This program draws a graph and identifies turning points.
"""
from graphics import *


def main():
    window_height = 600
    window = GraphWin('Graph', 800, window_height)

    # Open the input file and read the number of points
    pointsfile = open("points.txt", "r")
    num_points = int(pointsfile.readline())

    x = 20
    first_y = int(pointsfile.readline())  # get the first y-coordinate
    first_point = Point(x, window_height - first_y)

    x += 10
    second_y = int(pointsfile.readline())
    second_point = Point(x, window_height - second_y)

    line = Line(first_point, second_point)
    line.setOutline('orange')
    line.draw(window)

    '''circle = Circle(first_point, 3)
    circle.setFill('red')
    circle.draw(window)'''


    if second_y > first_y:
        increasing = True
        '''print(first_y, "is a valley. ")
        circle = Circle(first_point, 3)
        circle.setFill('blue')
        circle.draw(window)'''

    else:
        increasing = False  # in other words, we're decreasing
        '''print(first_y, " is a peak. ")
        circle = Circle(first_point, 3)
        circle.setFill('red')
        circle.draw(window)'''

    if increasing == True:
        print(first_y, "is a valley. ")
        circle = Circle(first_point, 3)
        circle.setFill('blue')
        circle.draw(window)

    else:
        print(first_y, " is a peak. ")
        circle = Circle(first_point, 3)
        circle.setFill('red')
        circle.draw(window)

    first_y = second_y
    first_point = second_point



    for i in range(2, num_points):  # since we already did first 2
        # Read the next point and update x
        x += 10
        second_y = int(pointsfile.readline())
        second_point = Point(x, window_height - second_y)


        line = Line(first_point, second_point)
        line.setOutline('orange')
        line.draw(window)

        circle = Circle(first_point, 1)
        circle.draw(window)


        if increasing == True:
            if first_y > second_y:
                print(first_y, "is a peak. ")
                circle = Circle(first_point, 3)
                circle.setFill('red')
                circle.draw(window)

        if increasing == False:
            if first_y < second_y:
                print(first_y, " is a valley. ")
                circle = Circle(first_point, 3)
                circle.setFill('blue')
                circle.draw(window)

        increasing = second_y > first_y  # Think about why this works!

        first_y = second_y
        first_point = second_point


    if increasing == True:
        print(first_y, "is a peak. ")
        circle = Circle(first_point, 3)
        circle.setFill('red')
        circle.draw(window)

    else:
        print(first_y, " is a valley. ")
        circle = Circle(first_point, 3)
        circle.setFill('blue')
        circle.draw(window)



    window.getMouse()
    window.close()


main()
