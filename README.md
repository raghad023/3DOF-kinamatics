# 3DOF-kinematics
compute the inverse and forward kinematics for a robot with 3 degrees of freedom

## Forward Kinematics

Objective: Calculate the end-effector position \((x, y)\) given joint angles and link lengths.

## Formula:
x = L1 * cos(θ1) + L2 * cos(θ1 + θ2) + L3 * cos(θ1 + θ2 + θ3)
y = L1 * sin(θ1) + L2 * sin(θ1 + θ2) + L3 * sin(θ1 + θ2 + θ3)

## Example

Given:
θ1 = 30°
θ2 = 45°
θ3 = 60°
L1 = 5
L2 = 4
L3 = 3

θ1 = 30° = π/6 ≈ 0.5236 radians
θ2 = 45° = π/4 ≈ 0.7854 radians
θ3 = 60° = π/3 ≈ 1.0472 radians

x = L1 * cos(θ1) + L2 * cos(θ1 + θ2) + L3 * cos(θ1 + θ2 + θ3)
  = 5 * cos(0.5236) + 4 * cos(0.5236 + 0.7854) + 3 * cos(0.5236 + 0.7854 + 1.0472)
  = 5 * 0.866 + 4 * 0.574 + 3 * (-0.5)
  = 4.33 + 2.30 - 1.50
  = 5.13

y = L1 * sin(θ1) + L2 * sin(θ1 + θ2) + L3 * sin(θ1 + θ2 + θ3)
  = 5 * sin(0.5236) + 4 * sin(0.5236 + 0.7854) + 3 * sin(0.5236 + 0.7854 + 1.0472)
  = 5 * 0.5 + 4 * 0.819 + 3 * 0.866
  = 2.50 + 3.28 + 2.60
  = 8.38

## End-effector position: (x, y) = (5.13, 8.38)

## Inverse Kinematics

Objective: Calculate the joint angles \( θ1), \( θ2), and \( θ3) to reach a desired end-effector position \((x, y)\).

## Example
Given:

(x, y) = (5, 6)
L1 = 5
L2 = 4
L3 = 3

-Distance: √(5² + 6²) = 7.81
Intermediate = {Distance} - L1 = 7.81 - 5 = 2.81


θ1 = atan2(y, x) - atan2(L2 + L3, Intermediate)
   = atan2(6, 5) - atan2(7, 2.81)
   ≈ -0.33 radians

Adjusted Position = Intermediate - L1 * sin(θ1)
                  ≈ 2.81 - 5 * sin(-0.33)
                  ≈ 4.44

θ2 = atan2(y - L1 * sin(θ1), x - L1 * cos(θ1)) - atan2(L3, L2 + L3)
   ≈ atan2(6 + 1.63, 5 - 4.33) - atan2(3, 7)
   ≈ 0.82 radians

θ3 = atan2(y - L1 * sin(θ1) - L2 * sin(θ2), x - L1 * cos(θ1) - L2 * cos(θ2))
   ≈ atan2(6 - 5 * sin(-0.33) - 4 * sin(0.82), 5 - 5 * cos(-0.33) - 4 * cos(0.82))
   ≈ 1.16 radians

## θ1 ≈ -0.33 radians ≈ -18.9 degrees
## θ2 ≈ 0.82 radians ≈ 47.0 degrees
## θ3 ≈ 1.16 radians ≈ 66.5 degrees

