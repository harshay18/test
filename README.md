git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/harshay18/test.git
git push -u origin main



ok bro
hello

import numpy as np
import matplotlib.pyplot as plt

def generate_points(num_points):
    # Generate random points within a square [-1, 1] x [-1, 1]
    points = np.random.rand(num_points, 2) * 2 - 1
    return points

def is_inside_circle(x, y):
    # Check if a point (x, y) is inside the circle (unit circle centered at the origin)
    return x**2 + y**2 <= 1

def is_inside_square(x, y):
    # Check if a point (x, y) is inside the square
    return (-0.5 <= x <= 0.5) and (-0.5 <= y <= 0.5)

def monte_carlo_simulation(num_points):
    points = generate_points(num_points)

    circle_points = sum(1 for x, y in points if is_inside_circle(x, y))
    square_points = sum(1 for x, y in points if is_inside_square(x, y))

    circle_area = circle_points / num_points *4 # Area of the circle (pi * r^2, r=1)
    square_area = square_points / num_points *4  # Area of the square

    ratio_points = square_points / circle_points
    area_ratio = square_area / circle_area

    print(f"Estimated Area of Circle: {circle_area}")
    print(f"Estimated Area of Square: {square_area}")
    print(f"Ratio of Points in Square to Points in Circle: {ratio_points}")
    print(f"Ratio of Area of Square to Area of Circle: {area_ratio}")

    # Plot the points
    plt.figure(figsize=(8, 8))
    plt.scatter(points[:, 0], points[:, 1], c='blue', alpha=0.5, label='Generated Points')
    plt.scatter([point[0] for point in points if is_inside_circle(point[0], point[1])],
                [point[1] for point in points if is_inside_circle(point[0], point[1])],
                c='green', alpha=0.5, label='Inside Circle')
    plt.scatter([point[0] for point in points if is_inside_square(point[0], point[1])],
                [point[1] for point in points if is_inside_square(point[0], point[1])],
                c='red', alpha=0.5, label='Inside Square')

    plt.title('Monte Carlo Simulation for Circle and Square')
    plt.legend()
    plt.show()

# Number of points in the simulation
num_points = 100000

# Run the Monte Carlo simulation
monte_carlo_simulation(num_points)
