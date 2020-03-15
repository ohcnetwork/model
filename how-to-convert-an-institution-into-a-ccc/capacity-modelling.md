---
description: >-
  The first step each institution should do is to model the capacity that each
  individual institution can create and contribute to the CCC Network.
---

# Capacity Modelling

## Rules of Thumb

* [ ] Enter the number of types of rooms in the institution.
* [ ] Enter the dimensions of 1 bed
* [ ] Enter the dimensions of each room, and their respective number.
* [ ] Calculate Capacity

```
$ The rule of thumb is that each person needs 8Ft*4Ft area to sit and lie down.
```

 The system will give a capacity that can be then created at that center. Loyola has 36 classrooms where 1000 students study and 3 large exam halls.  
  
The School can then split the capacity into two parts.  
  
1. Quarantine Area  
2. Care Area

The Capacity of an institution can be found by running this python script.

{% code title="model.py" %}
```python
print("Finding Capacity of institution !\n")

# Getting number of types of rooms, and dimensions of bed
t_room = eval(input("How many types of rooms are present in your institution? "))
l_bed = eval(input("What is the length of 1 bed? [Larger Dimension] "))
b_bed = eval(input("What is the breadth of 1 bed? [Smaller Dimension] "))

capacity = [] # Holds list of room capacities
counter = 0 # Loop Counter

while (counter < t_room) : # While the counter is less than the number of types of rooms
    print("\n Calculating Capacity of Room ", counter)

    # Getting number of such rooms, and dimensions of room
    l_room = eval(input("What is the length of 1 room? [Larger Dimension] "))
    print("")
    b_room = eval(input("What is the breadth of 1 room? [Smaller Dimension] "))
    print("")
    n_room = eval(input("How many rooms of this size are in your institution? "))
    print("")

    # Checking whether dimensions match
    assert (l_room >= l_bed), "Dimensions of bed and room are invalid"
    assert (b_room >= b_bed), "Dimensions of bed and room are invalid"

    # Getting number of beds in a column
    n_bed_c = b_room//b_bed
    remainder = b_room % b_bed
    
    # Getting gap between beds in a column.
    if (remainder > 0.1):
        gap_c = (n_bed_c-1)/remainder
    else :
        if (n_bed_c > 2) :
            gap_c = (n_bed_c-2)/b_bed
            n_bed_c = n_bed_c -1
        else :
            gap_c = 0

    # Getting number of beds in a row
    n_bed_r = l_room // l_bed
    remainder = l_room % l_bed

    # Getting gap between beds in a row
    if (remainder > 0.1):
        gap_r = (n_bed_r-1)/remainder
    else :
        if (n_bed_r > 2) :
            gap_r = (n_bed_r-2)/b_bed
            n_bed_r = n_bed_r -1
        else :
            gap_r = 0
    # Calculating Capacities
    s_cap = n_bed_c * n_bed_r
    t_cap = s_cap * n_room

    print("In room ", 0, "\n In 1 row you can have", n_bed_r, "beds with %.2f" % round(gap_r, 2), "units gap between them.\n In 1 column you can have", n_bed_c, "beds with %.2f" % gap_c, "units gap between them.")
    print(" Capacity of 1 such room is ", s_cap)
    print(" Total Capacity of all such rooms is ", t_cap)

    capacity.append(int(t_cap)) # Add to list of capacities

    counter = counter + 1

print("\nList of total capacities is ", str(capacity))
print("Capacity of institution is ", sum(capacity))
```
{% endcode %}



