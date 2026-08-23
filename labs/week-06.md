# ISYS5002 - Week 6

Remember our little [weather program from Week 3](week-03.md)?

So far, it has only ever dealt with **one** reading at a time: the user types a temperature, we make a decision about it, and then the program ends. This week we're going to push ahead, from one, to **many**.

First, we'll use a **list** to hold many readings in a single variable. Then we'll use **loops** to work through those many readings, and to keep our menu running until the user actually chooses to exit.

## 1. Storing Many Readings in a List

### Step 1: Why We Need Lists

Imagine you want to record the temperature for each day of the week. Using what we know so far, you might write something like this:

```python
monday = 18
tuesday = 22
wednesday = 25
thursday = 19
friday = 30
saturday = 27
sunday = 21
```

This works, but it is awkward. Try to answer these questions using only the code above:

- What was the average temperature for the week?
- How many days were above 25°C?
- What if we now want a fortnight of data instead of a week?

Each question would need you to type out all seven variable names again, and the last one would mean writing seven more variables by hand. There is a better way.

**Tip:** Whenever you find yourself copying and pasting a line of code and changing just one small thing each time, that is a strong hint that a list, a loop, or a function would serve you better.

There's a saying, `D.R.Y.` (don't repeat yourself!)

### Step 2: Creating a List

A **list** stores multiple values in a single variable. We write it using square brackets, with the values separated by commas.

```python
# One variable holding seven readings
temperatures = [18, 22, 25, 19, 30, 27, 21]
print(temperatures)
```

Output:

```
[18, 22, 25, 19, 30, 27, 21]
```

Lists can hold text just as happily as numbers:

```python
conditions = ["sunny", "sunny", "cloudy", "rain", "sunny", "windy", "cloudy"]
print(conditions)
```

**Tip:** Give your list a **plural** name (`temperatures`, not `temperature`). Don't mislead people reading your code..

### Step 3: Getting Items Out of a List

Each item in a list has a position, called its **index**. Python starts counting at **zero**, so the first item is at index `0`.

```python
temperatures = [18, 22, 25, 19, 30, 27, 21]

print("First reading:", temperatures[0])
print("Third reading:", temperatures[2])
print("Last reading:", temperatures[-1])
```

Output:

```
First reading: 18
Third reading: 25
Last reading: 21
```

Notice two things:

- `temperatures[2]` gives the **third** item, because counting starts at zero.
- A negative index counts backwards from the end, so `[-1]` is a convenient way to say "the last one" without knowing how long the list is.

The `len()` function tells you how many items a list contains:

```python
print("Number of readings:", len(temperatures))
```

**Tip:** If a list has 7 items, the valid indexes are `0` to `6`. Asking for `temperatures[7]` will raise an `IndexError`. Getting this off by one is so common that programmers have a name for it: an **off-by-one error** (`O.B.O.E.`).

### Step 4: Changing a List

Lists can be modified after they are created.

```python
temperatures = [18, 22, 25, 19, 30, 27, 21]

# Correct Thursday's reading
temperatures[3] = 20

# Add a new reading to the end
temperatures.append(24)

print(temperatures)
print("Now we have", len(temperatures), "readings.")
```

Output:

```
[18, 22, 25, 20, 30, 27, 21, 24]
Now we have 8 readings.
```

`append()` is a method—a function that belongs to the list—just like `.upper()` belonged to a string back in Week 2. It adds a single item to the end.

### Step 5: Debugging Common List Errors

Each snippet below contains one mistake. Run it first so you can read the error message, then fix it. Remember, the error message usually tells you exactly which line to look at.

```python
readings = [12, 15, 18]
print(readings[3])
```

```python
readings = (12, 15, 18)
readings.append(21)
```

```python
readings = [12, 15, 18]
print("The average is", readings / 3)
```

> **Hint for the second one:** Round brackets create a **tuple**, which is a close cousin of the list but cannot be changed after it is created. Sometimes that is exactly what you want, but not here.

### Challenge: Build Your Own Reading List

- Create a list of the humidity readings for a week (use made-up values for now).
- Print the first and last readings, using a negative index for the last one.
- Correct one of the readings by assigning a new value to its index.
- Add two more readings with `append()`, then print the length of the list.

**Extension:** Investigate what `temperatures[1:4]` does. This is called **slicing**. Can you use it to print just the weekend readings?

## 2. Working Through a List with `for`

### Step 1: Your First `for` Loop

A `for` loop takes each item in a list in turn and runs the same block of code for it.

```python
temperatures = [18, 22, 25, 19, 30, 27, 21]

for temperature in temperatures:
    print("Reading:", temperature)
```

Output:

```
Reading: 18
Reading: 22
Reading: 25
Reading: 19
Reading: 30
Reading: 27
Reading: 21
```

Read that first line as a sentence: "for each temperature in temperatures". The variable `temperature` is created by the loop, and on each pass it holds the next item from the list.

**Tip:** Just like if-else in Week 3, the colon (`:`) at the end of the line introduces an indented **block**. Everything indented under the `for` line runs once per item. Anything not indented runs only after the loop has finished entirely.

Predict the output of this code before you run it:

```python
for temperature in [10, 20, 30]:
    print("Checking...")
    print(temperature)
print("Done!")
```

How many times does "Checking..." appear? How many times does "Done!" appear? Run it and see whether your prediction was right.

### Step 2: Looping a Fixed Number of Times with `range()`

Sometimes you don't have a list BUT you still want to repeat something a set number of times. `range()` can help you out!

```python
for day_number in range(1, 8):
    print("Day", day_number)
```

Output:

```
Day 1
Day 2
Day 3
Day 4
Day 5
Day 6
Day 7
```

Note that `range(1, 8)` stops **before** 8. The end value is excluded, which trips up almost everyone at first. `range(5)` on its own starts at zero and gives you `0, 1, 2, 3, 4`—five numbers, which is often exactly what you need for indexing a list of five items.

We can combine `range()` with `len()` when we need the position as well as the value:

```python
temperatures = [18, 22, 25, 19, 30, 27, 21]

for index in range(len(temperatures)):
    print("Day", index + 1, "was", temperatures[index], "°C")
```

**Tip:** If you only need the values, use the simple `for temperature in temperatures:` form—it is clearer and cannot produce an `IndexError`. Reach for `range(len(...))` only when you genuinely need the index too.

### Step 3: Accumulating a Result

A very common pattern is to build up a result as the loop runs. We start with an "empty" value before the loop, then update it on each pass. This is called an **accumulator**.

**Pseudocode:**

```
set total to 0
for each temperature in temperatures:
    add the temperature to total
after the loop, divide total by the number of readings
```

**Code:**

```python
temperatures = [18, 22, 25, 19, 30, 27, 21]

total = 0
for temperature in temperatures:
    total = total + temperature

average = total / len(temperatures)
print("Total:", total)
print("Average:", average)
```

Output:

```
Total: 162
Average: 23.142857142857142
```

Look carefully at the indentation. `total = total + temperature` is **inside** the loop, so it runs seven times. The two `print()` calls are **outside** it, so they run once, after all the adding is finished. Try indenting the `average` line to match the loop and see what changes—this is a mistake worth making deliberately once so you recognise it later.

**Tip:** `total = total + temperature` can be shortened to `total += temperature`. The two mean exactly the same thing.

> **Advanced Note:** Python has built-in shortcuts for the most common accumulations: `sum(temperatures)`, `min(temperatures)`, `max(temperatures)`, and `len(temperatures)`. Use them in your own code from now on—but it is worth writing the loop by hand once, so you understand what the shortcut is doing on your behalf.

### Step 4: Selection Inside Repetition

Now we combine this week's loops with last month's if-else statements. Here we count how many days were hot, and collect those readings into a new list.

```python
temperatures = [18, 22, 25, 19, 30, 27, 21]

hot_days = 0
hot_readings = []

for temperature in temperatures:
    if temperature > 25:
        hot_days = hot_days + 1
        hot_readings.append(temperature)

print("Number of hot days:", hot_days)
print("Hot readings:", hot_readings)
```

Output:

```
Number of hot days: 2
Hot readings: [30, 27]
```

Notice that `hot_readings` starts as an **empty list** (`[]`) and grows as the loop finds matching readings. This filtering pattern is extremely useful, and you will reach for it constantly.

### Step 5: Sample Code Walkthrough

Let's trace the accumulator loop from Step 3 with a shorter list, `[10, 20, 30]`. Before the loop begins, `total` is 0.

- **Pass 1:** `temperature` is 10, so `total` becomes 0 + 10 = 10.
- **Pass 2:** `temperature` is 20, so `total` becomes 10 + 20 = 30.
- **Pass 3:** `temperature` is 30, so `total` becomes 30 + 30 = 60.

The list is now exhausted, so the loop ends. `total` is 60 and `len()` is 3, giving an average of 20.0.

**Tip:** When a loop misbehaves, add a temporary `print()` inside it to show the loop variable and your accumulator on every pass. Tracing by hand or by printing is one of the most reliable debugging techniques you have.

### Challenge: Weekly Weather Report

Using your list of readings, write a program that reports:

- The highest and lowest reading of the week.
- The average reading, rounded to one decimal place (investigate the `round()` function).
- How many days were above the average.
- A message for each day, using the if-else logic you wrote in Week 3, so that a single run prints advice for every day of the week.

**Extension:** Reuse the modular approach from Week 4. Write a function `def average(readings):` that takes a list and returns the mean, and another `def count_above(readings, threshold):`. Your main program should then be only a few lines long.

## 3. Repeating Until the User Is Done: `while`

A `for` loop is the right choice when you know how many times to repeat—once per item, or a fixed number of passes. But our weather menu has a different shape: we want to keep showing it **until** the user chooses to exit, and we have no idea how many choices they will make first. That calls for a `while` loop.

### Step 1: The Menu That Keeps Going

Back in Weeks 2 and 3 our menu displayed once and then the program ended. Let's finally fix that.

**Pseudo-code:**

```
repeat forever:
    display the weather menu
    get the user's choice
    if the choice is "4":
        say goodbye and stop repeating
    otherwise:
        respond to the choice
```

**Code:**

```python
while True:
    print()
    print("Weather Menu:")
    print("1. Check Temperature")
    print("2. Check Humidity")
    print("3. Check Wind Speed")
    print("4. Exit")

    choice = input("Enter your choice (1-4): ")

    if choice == "1":
        print("You chose to check the temperature.")
    elif choice == "2":
        print("You chose to check the humidity.")
    elif choice == "3":
        print("You chose to check the wind speed.")
    elif choice == "4":
        print("Goodbye!")
        break
    else:
        print("Invalid choice. Please select a valid option.")
```

Two new pieces of vocabulary here:

- `while True:` means "keep repeating this block indefinitely". The condition is always true, so the loop never ends on its own.
- `break` immediately exits the loop, skipping any remaining passes. It is our escape hatch.

### Step 2: A Word of Warning About Infinite Loops

A `while` loop that never reaches its exit condition will run forever. This will happen to you at some point, so it is worth knowing how to escape:

- **Colab / Jupyter:** press the stop (interrupt) button beside the cell.
- **Codespaces / VS Code terminal:** press `Ctrl` + `C`.

The most common cause is forgetting to change the variable that the condition depends on. Read this code but **do not run it**—can you see why it never stops?

```python
countdown = 5
while countdown > 0:
    print(countdown)
```

The fix is to make sure something inside the loop moves the condition towards being false:

```python
countdown = 5
while countdown > 0:
    print(countdown)
    countdown = countdown - 1
print("Liftoff!")
```

### Step 3: Collecting Readings Until the User Stops

Here is where lists and `while` loops work beautifully together. Instead of hard-coding our weather data, we can let the user enter as many readings as they like.

```python
readings = []

while True:
    entry = input("Enter a temperature, or type 'done' to finish: ")

    if entry == "done":
        break

    readings.append(float(entry))

print()
print("You entered", len(readings), "readings:", readings)

if len(readings) > 0:
    print("The average was", sum(readings) / len(readings))
else:
    print("No readings were entered.")
```

Notice the final if-else. If the user types `done` straight away, `readings` is empty and dividing by `len(readings)` would crash with a `ZeroDivisionError`!

### Step 4: Validating Input with a Loop

In Week 4 we used **pyinputplus** to keep asking until the user typed something valid. Now you can see how that library works internally—it is just a loop:

```python
while True:
    entry = input("Enter a whole number of degrees: ")
    if entry.isdigit():
        temperature = int(entry)
        break
    print("That doesn't look like a whole number. Please try again.")

print("Thank you. You entered", temperature)
```

### Challenge: The Complete Weather Station

Bring together everything from Weeks 2 through 6 into one program:

- A menu that loops until the user chooses to exit.
- A menu option that lets the user **add** a reading, appending it to a list.
- A menu option that **displays all readings so far**, using a `for` loop, numbered from 1.
- A menu option that shows **summary statistics**: count, average, highest, and lowest.
- Your Week 3 if-else advice ("It's cold – wear a jacket!" and so on) applied to whichever reading the user asks about.
- Sensible behaviour when the list is still empty.

**Tip:** Build this one option at a time and test as you go. Get the menu looping first, then add a single option, run it, and only then move on. Trying to write the whole thing before running any of it is a recipe for a long debugging session.

**Extension:** Use the decomposition skills from Week 4 to keep this readable. Aim for small functions such as `display_menu()`, `add_reading(readings)`, `show_readings(readings)`, and `show_statistics(readings)`, with the `while` loop in your main script doing little more than calling them.

### Reflection

- How did you decide between a `for` loop and a `while` loop in the final challenge?
- What happened when you got the indentation wrong inside a loop? How did that differ from the error messages you saw in Week 1?
- Where did you have to think about the empty list case? Are there other "edge cases" you have not handled yet?

### Summary

In this activity, we have covered:

- Store multiple values in a single **list** variable, and access them by **index** (remembering that counting starts at zero).
- Modify lists with index assignment and `append()`, and measure them with `len()`.
- Use a `for` loop to run the same block of code once per item, and `range()` to repeat a fixed number of times.
- Build up results with the **accumulator** pattern, and filter items by combining selection with repetition.
- Use a `while` loop with `break` to repeat until a condition is met.
- Recognise and escape an infinite loop.
