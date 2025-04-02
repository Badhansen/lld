# Design a Parking Lot - Single Thread

Write code for the low-level design of a parking lot with multiple floors.  
The parking lot has two kinds of parking spaces:  
- **Type = 2**: For 2-wheeler vehicles  
- **Type = 4**: For 4-wheeler vehicles  

There are multiple floors in the parking lot. On each floor, vehicles are parked in parking spots arranged in rows and columns.  
For simplicity, let's assume that each floor will have the same number of rows, and each row will have the same number of columns.

You can solve this question in either **Java** or **Python**.

---

## Methods to Implement in the `Solution` Class

### `init(Helper helper, int[][][] parking)`
- **Arguments**:
  - `helper`: Provides methods like `helper.print("")` and `helper.println("")` for printing logs.
  - `parking[i][j][k]`: Represents the parking spot at the `i-th` floor, `j-th` row, and `k-th` column.
- **Parking Spot Types**:
  - `4`: 4-wheeler parking spot
  - `2`: 2-wheeler parking spot
  - `0`: Inactive spot (no vehicle can be parked here)

---

### `park(int vehicleType, String vehicleNumber, String ticketId, int parkingStrategy)`
- **Returns**: `spotId` (e.g., `"floor-row-column"`)
- **Functionality**:
  - Assigns an empty parking spot to the vehicle.
  - Maps `vehicleNumber` and `ticketId` to the assigned `spotId`.
  - Example:  
    If `parking[2][0][15]` is the parking spot at the 2nd floor, 0th row, and 15th column, its `spotId` will be `"2-0-15"`.
- **Parking Strategies**:
  - **Strategy 0**:  
    Get the parking spot at the lowest index (lowest floor, row, and column).  
    Example:  
    If `park()` is called with `vehicleType = 4` and free 4-wheeler spots are at:  
    - `parking[0][0][0]`
    - `parking[0][0][1]`
    - `parking[1][0][2]`  
    The function will return `parking[0][0][0]` because it has the lowest index.
  - **Strategy 1**:  
    Get the floor with the maximum number of free spots for the given vehicle type.  
    If multiple floors have the same maximum free spots, choose the floor with the lowest index.  
    Example:  
    If `park()` is called with `vehicleType = 4` and:  
    - Floor 0 has 2 free 4-wheeler spots  
    - Floor 1 and Floor 3 both have 3 free 4-wheeler spots  
    The function will return the free 4-wheeler spot at the lowest index from Floor 1.

---

### `removeVehicle(String spotId)`
- **Returns**:  
  - `true` if the vehicle is successfully removed.  
  - `false` if the vehicle is not found or any other error occurs.
- **Functionality**:  
  Unparks or removes the vehicle from the parking spot.

---

### `String searchVehicle(String query)`
- **Returns**:  
  - The `spotId` where the vehicle is parked (e.g., `"2-0-15"`)  
  - An empty string (`""`) if the vehicle is not found.
- **Functionality**:  
  Searches for the latest parking details of a vehicle using either its `vehicleNumber` or `ticketId`.

---

### `int getFreeSpotsCount(int floor, int vehicleType)`
- **Returns**:  
  The number of free spots available for the given vehicle type (`2` or `4-wheeler`) on the specified floor.
- **Constraints**:  
  - `0 <= floor < parking.length` (from the `init()` method)

---

## Constraints
- **Vehicle Types**:
  - `type = 2`: For 2-wheeler vehicles
  - `type = 4`: For 4-wheeler vehicles
- **Parking Lot Dimensions**:
  - `1 <= floors <= 5`
  - `1 <= rows <= 10,000`
  - `1 <= columns <= 10,000`
  - `1 <= rows * columns <= 10,000`

---

## Input Example

```python
parking = [[
    [4, 4, 2, 2],
    [2, 4, 2, 0],
    [0, 2, 2, 2],
    [4, 4, 4, 0]
]]
```
## Example
- `park(2, "bh234", "tkt4534", 0)` will return `spotId`: `"0-0-2"`  
i.e., parking spot from floor 0, row 0, and column 2 is assigned.

- `search("bh234")` or `search("tkt4534")`  
At this point should return `spotId = "0-0-2"`  
i.e., we can use `vehicleNumber: "bh234"` or `ticketId: "tkt4534"` to find the parking spot id where the vehicle is parked.

- `getFreeSpotsCount(0, 2)`  
Will return `6`.

- `removeVehicle("0-0-2")`  
Should unpark the parked vehicle.

- `getFreeSpotsCount(0, 2)`  
After unparking, `getFreeSpotsCount` will now return `7`.