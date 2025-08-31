import math

def get_radius_from_char(c: str) -> int:
    """Converts a character ('1'-'9', 'A'-'Z') to a light source radius."""
    if '1' <= c <= '9':
        return int(c)
    elif 'A' <= c <= 'Z':
        return ord(c) - ord('A') + 10
    return 0

def get_char_from_brightness(b: int) -> str:
    """Converts a brightness value to its character representation ('0'-'9', 'A'-'Z')."""
    b = int(b)
    if b <= 9:
        return str(b)
    # Cap brightness at 35 ('Z')
    elif b >= 35:
        return 'Z'
    else:
        return chr(ord('A') + b - 10)

# Step 1: Read dimensions and identify light sources
# l, w, d for length, width, depth.
l = int(input())
w = int(input())
d = int(input())
n = int(input())

sources = []
# Use a structured loop to read input
for z in range(d):
    for y in range(w):
        line = input()
        for x, char in enumerate(line):
            if char != '.':
                radius = get_radius_from_char(char)
                # Store sources as (x, y, z, radius) tuples
                sources.append((x, y, z, radius))
    if z < d - 1:
        try:
            input() # Consume the blank line separator
        except EOFError:
            pass

# Step 2: Create a new grid for brightness, initialized to all zeros
brightness_grid = [[[0 for _ in range(l)] for _ in range(w)] for _ in range(d)]

# Step 3: Calculate brightness for every cell
for z_target in range(d):
    for y_target in range(w):
        for x_target in range(l):
            total_brightness = 0
            # Sum the brightness contribution from every source
            for x_source, y_source, z_source, radius in sources:
                distance = math.sqrt((x_target - x_source)**2 + (y_target - y_source)**2 + (z_target - z_source)**2)
                brightness = radius - round(distance)
                
                if brightness > 0:
                    total_brightness += brightness
            
            brightness_grid[z_target][y_target][x_target] = total_brightness

# Step 4: Print the formatted output grid
for z in range(d):
    if z > 0:
        print() # Print a blank line between depth levels
    for y in range(w):
        output_line = "".join([get_char_from_brightness(brightness_grid[z][y][x]) for x in range(l)])
        print(output_line)
