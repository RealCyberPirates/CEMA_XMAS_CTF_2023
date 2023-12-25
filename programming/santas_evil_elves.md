# Santa's Evil Elves

Description

Back by dope demand, Evil elves are attacking Santa's workshop. Luckily, Santa just bought a tank. However, he's facing a problem with aiming. The challenge is to help Santa shoot the elves. Successfully hitting all targets earns a reward.

Challenge Address: `167.172.109.120:3333`

## Approach

The challenge involves calculating the correct projectile speed to hit elves at varying distances and heights using a tank cannon.

1. Connecting to the Challenge Server:
    - Utilize Python's socket library to connect to the server at 167.172.109.120 on port 3333.
2. Parsing Challenge Data:
    - Read the distance and height data for each elf from the server's response.
    - Regular expressions (re library) were used to extract these values.
3. Physics Calculation:
    - The problem is a classic projectile motion scenario.
    - Calculate the initial speed required for the projectile to reach a given distance and height, considering gravity's influence (981 m/s²).
    - Use a numerical method (fsolve from SciPy) to solve the projectile motion equations.
4. Solution Submission:
    - After calculating the required speed, format it to two decimal places and send it back to the server.
    - Wait for the server's response to confirm if the hit was successful.
5. Iterative Process:
    - Repeat the process for each level of the challenge.

```python
import socket
import re
import math

def calculate_muzzle_velocity(elevation, distance):
    print(f"elevation: {elevation} distance: {distance}")
    earth_g = 9.81  # Acceleration due to gravity
    fall_time = math.sqrt(2 * elevation / earth_g)
    return distance / fall_time

def main():
    calculate_muzzle_velocity(56, 1024)
    print("Let's shoot some elves shall we?")

    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect(("167.172.109.120", 3333))
        while True:
            buf = s.recv(2048).decode()
            if not buf:
                break
            print(f"Buf: {buf}")

            if "Press enter to start..." in buf:
                s.send(b"\n")

            if "(in m/s)" in buf:
                re_height_distance = re.compile(r"([0-9]+)m")
                results = re_height_distance.findall(buf)

                if len(results) >= 2:
                    height, distance = map(float, results[:2])
                    print(f"Height: {height} Distance: {distance}")
                    muzzle_speed = calculate_muzzle_velocity(height, distance)
                    print(f"Required speed: {muzzle_speed:.2f}")
                    s.sendall(f"{muzzle_speed:.2f}\n".encode())
                else:
                    print("Failed to parse height and distance")

if __name__ == "__main__":
    main()
```

The script needed to be executed a few time due to strange rounding quirks.

```sh
How fast should he shoot his cannon? (in m/s)


Height: 71.0 Distance: 1770.0
elevation: 71.0 distance: 1770.0
Required speed: 465.23
Buf: Correct!
Buf: 
Level 20/20


         ☻/╦╤─
    ░░░░███████ ]▄▄▄▄▄▄▄▄ 
    ▂▄▅█████████▅▄▃▂ 
   [███████████████████].
     ◥⊙▲⊙▲⊙▲⊙▲⊙▲⊙▲⊙◤.. 
    ===========================
                           ↑  |
                           |  |
                           |  |
                        45m|  |
                           |  |                                                   [◣_◢] 
                           |  |                                                   /()\    
                           ↓  |____________________________________________________/\ 
                              ←-----------------------------------------------------→
                                                       5706m
    

How fast should he shoot his cannon? (in m/s)


Height: 45.0 Distance: 5706.0
elevation: 45.0 distance: 5706.0
Required speed: 1883.84
Buf: Correct!
Buf: 
You did well my young padawan, here's your reward:

Congrats, you killed all the evil elfs, here's your reward: D

-----------------------------------------
CEMA{H1gh_K1net1c_Solut1ons_Are_Fun}
-----------------------------------------
```

## Flag

`CEMA{H1gh_K1net1c_Solut1ons_Are_Fun}`
