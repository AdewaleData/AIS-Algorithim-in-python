import random
import math

# Define the problem function
def problem(x):
    return math.sin(x)/x

# Define the AIS parameters
num_antigens = 10
num_antibodies = 50
mutation_rate = 0.1
num_iterations = 1000

# Define the AIS functions
def initialize_population():
    antigens = [random.uniform(0, 10) for i in range(num_antigens)]
    antibodies = [random.uniform(antigens[i]-1, antigens[i]+1) for i in range(num_antigens) for j in range(num_antibodies//num_antigens)]
    return antigens, antibodies

def calculate_affinity(antigen, antibody):
    return -abs(antibody - antigen)

def select_antibodies(antigens, antibodies):
    affinities = [[i, j, calculate_affinity(antigens[i], antibodies[j])] for i in range(num_antigens) for j in range(num_antibodies)]
    affinities = sorted(affinities, key=lambda x: x[2], reverse=True)
    selected_antibodies = [affinities[i][1] for i in range(num_antibodies)]
    return selected_antibodies

def mutate_antibodies(selected_antibodies):
    mutated_antibodies = [selected_antibodies[i] + random.gauss(0, mutation_rate * 10) for i in range(num_antibodies)]
    return mutated_antibodies

def update_population(antigens, antibodies, selected_antibodies, mutated_antibodies):
    for i in range(num_antibodies):
        for j in range(num_antigens):
            if calculate_affinity(antigens[j], mutated_antibodies[i]) > calculate_affinity(antigens[j], antibodies[i]):
                antibodies[i] = mutated_antibodies[i]
                break
    return antibodies

# Run the AIS algorithm
antigens, antibodies = initialize_population()

for iteration in range(num_iterations):
    selected_antibodies = select_antibodies(antigens, antibodies)
    mutated_antibodies = mutate_antibodies([antibodies[i] for i in selected_antibodies])
    antibodies = update_population(antigens, antibodies, selected_antibodies, mutated_antibodies)

best_antibody = max(antibodies, key=problem)
print("Best solution found: x = {}, f(x) = {}".format(best_antibody, problem(best_antibody)))
