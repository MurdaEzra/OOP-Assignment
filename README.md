# OOP-Assignment

 Base class: Smartphone

class Smartphone:
    def __init__(self, brand, model, battery_percentage, operating_system):
        self.brand = brand  # Brand of the smartphone
        self.model = model  # Model of the smartphone
        self.battery_percentage = battery_percentage  # Battery percentage
        self.operating_system = operating_system  # Operating system (e.g., Android, iOS)

    def make_call(self, phone_number):
        if self.battery_percentage > 0:
            print(f"Making a call to {phone_number}...")
            self.battery_percentage -= 5  # Decrease battery after making a call
        else:
            print("Battery is too low to make a call!")

    def send_message(self, phone_number, message):
        if self.battery_percentage > 0:
            print(f"Sending message to {phone_number}: {message}")
            self.battery_percentage -= 2  # Decrease battery after sending a message
        else:
            print("Battery is too low to send a message!")

    def charge(self, amount):
        self.battery_percentage = min(self.battery_percentage + amount, 100)  # Cap battery at 100%
        print(f"Charging... Battery is now at {self.battery_percentage}%.")

    def __str__(self):
        return f"Smartphone {self.brand} {self.model} with {self.operating_system}, Battery: {self.battery_percentage}%"

# Subclass: GamingPhone (inherits from Smartphone)

class GamingPhone(Smartphone):
    def __init__(self, brand, model, battery_percentage, operating_system, gaming_mode=False):
        # Calling the constructor of the superclass (Smartphone)
        super().__init__(brand, model, battery_percentage, operating_system)
        self.gaming_mode = gaming_mode  # Whether the gaming mode is enabled

    def toggle_gaming_mode(self):
        self.gaming_mode = not self.gaming_mode
        mode = "enabled" if self.gaming_mode else "disabled"
        print(f"Gaming mode {mode}.")
    
    def make_call(self, phone_number):
        if self.gaming_mode:
            print("Cannot make a call while gaming mode is enabled.")
        else:
            super().make_call(phone_number)  # Call the parent class method if gaming mode is not enabled

    def __str__(self):
        return f"GamingPhone {self.brand} {self.model} with {self.operating_system}, Battery: {self.battery_percentage}%, Gaming Mode: {'On' if self.gaming_mode else 'Off'}"


# Creating an object for Murda smartphone (Smartphone class)

murda_phone = Smartphone("Murda", "X1000", 50, "Android")

# Creating an object for a GamingPhone
gaming_phone = GamingPhone("Murda", "X1000 Pro", 80, "Android", gaming_mode=False)

# Displaying both phones
print(murda_phone)  # Display smartphone details
murda_phone.make_call("123-456-7890")  # Making a call

print("\n")

print(gaming_phone)  # Display gaming phone details
gaming_phone.toggle_gaming_mode()  # Enabling gaming mode
gaming_phone.make_call("123-456-7890")  # Attempt to make a call with gaming mode enabled
gaming_phone.toggle_gaming_mode()  # Disabling gaming mode
gaming_phone.make_call("123-456-7890")  # Making a call after disabling gaming mode

# Charging the phones
murda_phone.charge(30)
gaming_phone.charge(10)
