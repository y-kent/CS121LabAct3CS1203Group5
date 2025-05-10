# **CS 121 Lab3**
## by: Group 5
___
### Always Remember:
![alt text](bible-verses-about-hope-1-1585157294-1.jpg) 
___
### Group 5 Members and their Subclass:
| Members                | Subclass                 | 
| ---------------------- | :----------------------: |
| Macatangay, Alwyn Kent | Sofa                     | 
| Manalo, Cris Julian    | Bookshelf                | 
| Raras, Janna Alexis    | Dining Table             |
| Villan, John David     | Bed                      |
___
# OVERVIEW
> This Python program simulates assembling and interacting with different types of furniture
### The Subclasses used:
```
Sofa
```
```python
class Sofa(Furniture):
    def __init__(self, material, style, size, weight_limit, leg_rest=False, position="not seated"):
        super().__init__("Sofa", material, style, size, weight_limit)
        self.assembly_time = 9
        self.disassemble_time = 5        
        self.leg_rest = leg_rest
        self.position = position

    def assemble(self):
        if not self.is_assembled:
            print(f"Starting to assemble the {self.furniture_type} made of {self.material}...")
            if assemble_sound:
                assemble_sound.play()
            for i in range(self.assembly_time):
                print(".", end="", flush=True)
                time.sleep(0.25)
            print()
            self.is_assembled = True
            print(f"\nFinished assembling the {self.furniture_type} made of {self.material}.")
        else:
            print(f"The {self.furniture_type} is already assembled.")

    def use(self):
        if self.is_assembled:
            print(f"You are using the {self.furniture_type}.")
            self.adjust_position()
        else:
            print(f"The {self.furniture_type} must be assembled before use.")

    def sit(self):
        if self.position != "sitting":
            self.position = "sitting"
            print("You sit upright on the sofa.")
            if sit_sound:
                sit_sound.play()
        else:
            print("You are already sitting.")

    def lay_down(self):
        if self.position != "laying":
            self.position = "laying"
            print("You lay down on the sofa.")
            if laydown_sound:
                laydown_sound.play()
        else:
            print("You are already lying down.")

    def extend_leg_rest(self):
        if not self.leg_rest:
            self.leg_rest = True
            print("Leg rest extended.")
            if openleg_rest_sound:
                openleg_rest_sound.play()
        else:
            print("Leg rest is already extended.")

    def retract_leg_rest(self):
        if self.leg_rest:
            self.leg_rest = False
            print("Leg rest retracted.")
            if closeleg_rest_sound:
                closeleg_rest_sound.play()
        else:
            print("Leg rest is already retracted.")

    def adjust_position(self):
        while True:
            print("\n============================================")
            print("What would you like to do?")
            print("a. Sit")
            print("b. Lay down")
            print("c. Extend leg rest")
            print("d. Retract leg rest")
            print("e. Leave")
            print("============================================\n")
            choice = input("Enter your choice (a/b/c/d/e): ").lower()
            if choice == "a":
                self.sit()
            elif choice == "b":
                self.lay_down()
            elif choice == "c":
                self.extend_leg_rest()
            elif choice == "d":
                self.retract_leg_rest()
            elif choice == "e":
                if self.leg_rest:
                    print("You cannot leave the sofa while the leg rest is extended.")
                    print("Please retract it first.")
                else:
                    print("Leaving the sofa...")
                    break
            else:
                print("Invalid option. Please select again.")

    def disassemble(self):
        if self.is_assembled:
            print(f"Starting to disassemble the {self.furniture_type}...")
            if disassemble_sound:
                disassemble_sound.play()
            for i in range(self.disassemble_time):
                print(".", end="", flush=True)
                time.sleep(0.25)
            print()
            self.is_assembled = False
            print(f"The {self.furniture_type} has been disassembled.")
        else:
            print(f"The {self.furniture_type} is already disassembled.")

    def instruction(self):
        print("""
============================================
Sofa Assembly Instructions:
1. Lay out all parts: Armrests (2), Base frame, Backrest, Cushions, Legs (4), Screws & Bolts.
2. Attach armrests to base using dowels and bolts.
3. Secure backrest with screws.
4. Screw in the legs.
5. Place cushions in position.

Estimated time: 45–60 minutes.
============================================
""")
```
```
Dining Table
```
```python
class DiningTable(Furniture):
    def __init__(self, material, style, size, weight_limit):
        super().__init__("Dining Table", material, style, size, weight_limit)
        self.assembly_time = 9
        self.disassemble_time = 5
        self.design_items = []
        self.is_set_up = False

    def assemble(self):
        if not self.is_assembled:
            print(f"Starting to assemble the {self.furniture_type} made of {self.material}...")
            if assemble_sound:
                assemble_sound.play()
            for i in range(self.assembly_time):
                print(".", end="", flush=True)
                time.sleep(0.25)
            print()
            self.is_assembled = True
            print(f"\nFinished assembling the {self.furniture_type} made of {self.material}.")
        else:
            print(f"The {self.furniture_type} is already assembled.")

    def use(self):
        if self.is_assembled:
            print(f"Using the {self.furniture_type}.")
            self.table_actions()
        else:
            print(f"The {self.furniture_type} must be assembled before use.")

    def disassemble(self):
        if self.is_assembled:
            print(f"Starting to disassemble the {self.furniture_type}...")
            if disassemble_sound:
                disassemble_sound.play()
            for i in range(self.disassemble_time):
                print(".", end="", flush=True)
                time.sleep(0.25)
            print()
            self.is_assembled = False
            print(f"The {self.furniture_type} has been disassembled.")
        else:
            print(f"The {self.furniture_type} is already disassembled.")

    def instruction(self):
        print("""
============================================
Dining Table Assembly Instructions:
1. Unpack components: Tabletop, Legs (4), Cross-support bar, Screws/Bolts.
2. Attach legs to the tabletop using bolts and a wrench.
3. Install cross-support bar.
4. Tighten all fasteners.

Estimated time: 30 minutes.
============================================
""")

    def set_up(self):
        if not self.is_set_up:
            self.is_set_up = True
            print(f"Setting up the table.")
        else:
            print(f"The table is already set up.")

    def design(self, design_items):
        self.design_items.extend(design_items)
        print(f"Design items added: {', '.join(design_items)}")

    def check_table(self):
        print("Table Design and Setup Details:")
        print(f"Design added: {', '.join(self.design_items) if self.design_items else 'No designs added.'}")
        print(f"Table setup: {'Done' if self.is_set_up else 'Not Yet'}")

    def table_actions(self):
        while True:
            print("\n============================================")
            print("What would you like to do?")
            print("a. Add Design")
            print("b. Set-up Table")
            print("c. Check Table")
            print("d. Leave")
            print("============================================\n")
            action = input("Choose an action: ").lower()
            if action == 'a':
                design_items = input("What design do you want to add? (comma separated): ").split(',')
                self.design([item.strip() for item in design_items])
            elif action == 'b':
                self.set_up()
            elif action == 'c':
                self.check_table()
            elif action == 'd':
                print("Leaving the Dining Table.")
                break
            else:
                print("Invalid choice. Please select again.")
```
```
Bookshelf
```
```python
class Bookshelf(Furniture):
    def __init__(self, material, style, size, weight_limit, shelves=5):
        super().__init__("Bookshelf", material, style, size, weight_limit)
        self.assembly_time = 9
        self.disassemble_time = 5
        self.shelves = shelves
        self.books = []

    def assemble(self):
        if not self.is_assembled:
            print(f"Starting to assemble the {self.furniture_type} made of {self.material}...")
            if assemble_sound:
                assemble_sound.play()


            for i in range(self.assembly_time):
                print(".", end="", flush=True)
                time.sleep(0.25)
            print()
            self.is_assembled = True
            print(f"\nFinished assembling the {self.furniture_type} made of {self.material}.")
        else:
            print(f"The {self.furniture_type} is already assembled.")

    def use(self):
        if not self.is_assembled:
            print(f"The {self.furniture_type} must be assembled before use.")
            return

        while True:
            print("\n============================================")
            print("Bookshelf Menu:")
            print("a. Add a book")
            print("b. Remove a book")
            print("c. View bookshelf")
            print("d. Exit")
            print("============================================\n")
            choice = input("Enter your choice (a/b/c/d): ").lower()
            if choice == "a":
                book = input("Enter the name of the book to add: ").strip()
                if book:
                    self.books.append(book)
                    print(f"'{book}' has been added to the bookshelf.")
                    if add_book_sound:
                        add_book_sound.play()
                else:
                    print("Book name cannot be empty.")
            elif choice == "b":
                book = input("Enter the name of the book to remove: ").strip()
                if book in self.books:
                    self.books.remove(book)
                    print(f"'{book}' has been removed from the bookshelf.")
                    if add_book_sound:
                        add_book_sound.play()
                else:
                    print(f"'{book}' not found in the bookshelf.")
            elif choice == "c":
                if self.books:
                    print("\nBooks currently in the bookshelf:")
                    for idx, b in enumerate(self.books, start=1):
                        print(f"{idx}. {b}")
                else:
                    print("The bookshelf is empty.")
            elif choice == "d":
                print("Exiting bookshelf menu...")
                break
            else:
                print("Invalid option. Please select again.")

    def disassemble(self):
        if self.is_assembled:
            print(f"Starting to disassemble the {self.furniture_type}...")
            if disassemble_sound:
                disassemble_sound.play()
            for i in range(self.disassemble_time):
                print(".", end="", flush=True)
                time.sleep(0.25)
            print()
            self.is_assembled = False
            print(f"The {self.furniture_type} has been disassembled.")
        else:
            print(f"The {self.furniture_type} is already disassembled.")

    def instruction(self):
        print(f"""
============================================
Bookshelf Assembly Instructions:
1. Lay out all parts: Side panels (2), Shelves ({self.shelves}), Back panel, Screws & Bolts.
2. Attach side panels to bottom shelf.
3. Install remaining shelves evenly spaced.
4. Attach back panel with screws.
5. Secure all joints and place upright.

Estimated time: 1.5 - 2 hours.
============================================
""")
```
```
Bed
```
```python
class Bed(Furniture):
    def __init__(self, material, style, size, weight_limit):
        super().__init__("Bed", material, style, size, weight_limit)
        self.assembly_time = 9
        self.disassemble_time = 5
        self.has_sheets = False
        self.sleeping = False
        self.has_comforter = False

    def assemble(self):
        if not self.is_assembled:
            print(f"Starting to assemble the {self.furniture_type}...")
            if assemble_sound:
                assemble_sound.play()
            for i in range(self.assembly_time):
                print(".", end="", flush=True)
                time.sleep(0.25)
            print()
            self.is_assembled = True
            print(f"\nFinished assembling the {self.furniture_type} made of {self.material}.")
        else:
            print(f"The {self.furniture_type} is already assembled.")

    def use(self):
        if self.is_assembled:
            print(f"You are using the {self.furniture_type}.")
            self.bed_actions()
        else:
            print(f"The {self.furniture_type} must be assembled before use.")

    def bed_actions(self):
        while True:
            print("\n============================================")
            print("Bed Options:")
            print("a. Sleep")
            print("b. Wake up")
            print("c. Put on sheets")
            print("d. Remove sheets")
            print("e. Put Comforter On")
            print("f. Remove Comforter")
            print("g. Status")
            print("h. Leave")
            print("============================================\n")
            action = input("Choose an action: ").lower()
            if action == "a":
                if not self.sleeping:
                    print("You are now sleeping...")
                    if sleep_sound:
                        sleep_sound.play()
                    self.sleeping = True
                else:
                    print("You're already asleep.")
            elif action == "b":
                if self.sleeping:
                    print("You woke up!")
                    if awake_sound:
                        awake_sound.play()
                    self.sleeping = False
                else:
                    print("You're already awake.")
            elif action == "c":
                self.put_on_sheets()
            elif action == "d":
                self.remove_sheets()
            elif action == "e":
                self.put_on_comforter()
            elif action == "f":
                self.remove_comforter()
            elif action == "g":
                self.status()
            elif action == "h":
                if self.sleeping:
                    print("You can't leave the bed while sleeping. Wake up first.")
                else:
                    print("Leaving the bed...")
                    break
            else:
                print("Invalid choice. Please select again.")

    def put_on_sheets(self):
        if not self.is_assembled:
            print("You must assemble the bed before putting on sheets.")
        elif self.has_sheets:
            print("The bed already has sheets on.")
        else:
            self.has_sheets = True
            print("Sheets have been put on the bed.")

    def remove_sheets(self):
        if not self.has_sheets:
            print("There is no sheets to remove.")
        else:
            self.has_sheets = False
            print("Sheets have been removed from the bed.")

    def put_on_comforter(self):
        if not self.has_comforter:
            self.has_comforter = True
            print("You put a comforter on the bed.")
        else:
            print("The bed already has a comforter.")

    def remove_comforter(self):
        if self.has_comforter:
            self.has_comforter = False
            print("You remove the comforter from the bed.")
        else:
            print("There is no comforter to remove.")

    def disassemble(self):
        if self.is_assembled:
            print(f"Starting to disassemble the {self.furniture_type}...")
            if disassemble_sound:
                disassemble_sound.play()
            for i in range(self.disassemble_time):
                print(".", end="", flush=True)
                time.sleep(0.25)
            print()
            self.is_assembled = False
            print(f"\nThe {self.furniture_type} has been disassembled.")
        else:
            print(f"\nThe {self.furniture_type} is already disassembled")

    def status(self):
        print(f"\nExamining {self.furniture_type}...")

        if self.has_sheets:
            print("The bed has sheets.")
        else:
            print("The bed does not have sheets.")
   
        if self.has_comforter:
            print("The bed has a comforter.")
        else:
            print("The bed does not have a comforter.")
   
        if self.sleeping:
            print("Someone is sleeping on the bed.")
        else:
            print("There is no one on the bed currently.")
```
