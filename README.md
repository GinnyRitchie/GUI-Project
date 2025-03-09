import tkinter as tk
from tkinter import PhotoImage, messagebox

# ServiceWindow Class
class ServiceWindow:
    def __init__(self, master, name, services_content):
        self.master = master

        # Set up the Welcome window
        self.window = tk.Toplevel(master)
        self.window.title("Ginny Rose Studio :: Selfcare Service Info")
        self.window.config(bg="darkgreen")

        # Assign image to 'self.image' for Welcome window
        self.image = image_window
        tk.Label(self.window, image=self.image).pack()

        # Welcome message
        tk.Label(
            self.window,
            text=f"Welcome, {name}! Please click a service and hit submit to learn more about it!",
            bg="forestgreen",
            fg="white",
        ).pack(pady=10)

        # Service options as radio buttons
        self.service_var = tk.StringVar(value="Facial")
        services = [
            "Advanced Facials",
            "Permanent Jewelry",
            "Swedish Massages",
            "Spray Tans",
            "Body Waxing",
        ]
        for service in services:
            tk.Radiobutton(
                self.window, text=service, variable=self.service_var, value=service, bg="darkgreen", fg="white"
            ).pack(anchor=tk.W)

        # Submit and Back buttons
        tk.Button(self.window, text="Submit", command=self.submit, bg="white", fg="black").pack(pady=10)
        tk.Button(self.window, text="Back", command=self.go_back, bg="white", fg="black").pack(pady=5)

        self.services_content = services_content

    def submit(self):
        # Retrieve the selected service
        selected_service = self.service_var.get()

        # Debugging output to ensure correct service selection
        print(f"Selected service: {selected_service}")

        if selected_service in self.services_content:
            # Create a new Toplevel window for content display
            content_window = tk.Toplevel(self.window)
            content_window.title(f"{selected_service} Information")
            content_window.config(bg="darkgreen")
        
            # Add a scrollable Text widget
            text_widget = tk.Text(content_window, wrap="word", bg="darkgreen", fg="white", font=("Arial", 12))
            text_widget.insert("1.0", self.services_content[selected_service])  # Add the service content
            text_widget.config(state="disabled")  # Make the text read-only
            text_widget.pack(side="left", fill="both", expand=True, padx=10, pady=10)
        
            # Add a scrollbar
            scrollbar = tk.Scrollbar(content_window, command=text_widget.yview)
            scrollbar.pack(side="right", fill="y")
            text_widget.config(yscrollcommand=scrollbar.set)

            # Add a Close button
            tk.Button(
                content_window,
                text="Close",
                command=content_window.destroy,
                bg="white",
                fg="black"
            ).pack(pady=10)
        else:
            # Handle cases where the service is not in the dictionary
            messagebox.showerror(
                "Error",
                f"Service information for '{selected_service}' is not available."
            )

    def go_back(self):
        self.window.destroy()
        self.master.deiconify()

# Open the Service Window
def open_service_window():
    name = name_entry.get()
    if not name:
        messagebox.showerror("Error", "Name cannot be empty, please enter your name!")
        return

    root.withdraw()
    ServiceWindow(root, name, services_content)

# Main application window
root = tk.Tk()
root.title("Ginny Rose Studio :: Selfcare Services")
root.config(bg="darkgreen")

# Load and display the main image
image_main = PhotoImage(file="C:/Users/Ginny/Pictures/IMG_2641.png").subsample(4, 4)  # Main image
tk.Label(root, image=image_main).pack()

# Welcome message and name entry
tk.Label(
    root,
    text="Welcome, please enter your name and select any service to be prompted to the next page!",
    bg="darkgreen",
    fg="white",
).pack(pady=10)
tk.Label(root, text="Name", bg="darkgreen", fg="white").pack()

name_entry = tk.Entry(root)
name_entry.pack()

# Load the facial image for the Welcome window
image_window = PhotoImage(file="C:/Users/Ginny/Pictures/IMG_9398.png").subsample(8, 8)

# Dictionary containing service descriptions
services_content = {
    "Advanced Facials": "Advanced Facials include customized treatments that target specific skin concerns and include; double cleanses, exfoliation, extractions, facial massage, mask treatment with scalp, shoulder or hand massage, Celluma LED Therapy, serums, lip treatment, moisturizer and SPF. Prep; come in without makeup on and let your Esti know if you have any med or skincare changes. Aftercare; discontinue serums for 2 days, use SPF daily.",
    "Permanent Jewelry": "Permanent Jewelry involves custom-fitted 14K Gold Filled, Sterling Silver and Enamel bracelets, anklets and necklaces that are welded shut using a small welder with argon gas. If you need to break the chain for a medical procedure, cut the chain at the jump ring and bring it back in for a free re-weld.",
    "Body Waxing": "Body Waxing provides smooth and hair-free skin for 2-6 weeks. It is recommended to let hair grow 1/2 inch, exfoliate 2-3X per week, moisturize daily with pure aloe and rebook in 4-6 weeks for maintenance.",
    "Swedish Massages": "Swedish massages involve long, fluid strokes of muscles and tissues with a focus on relaxation and helping alleviate muscle tension.",
    "Spray Tans": "Spray Tans give you a natural-looking, sun-kissed glow without the UV exposure and can last 7-10 days with proper aftercare. Prep the skin by exfoliating and moisturizing days before your tan. The day of your tan; come in with loose clothes, no makeup, deoderant or lotion on. Aftercare; wait 5-12HRS to rinse, pat yourself dry and moisturize daily."

}

# Radiobuttons for service options
service_var = tk.StringVar(value="Facial")
services = ["Advanced Facials", "Permanent Jewelry", "Swedish Massages", "Spray Tans", "Body Waxing"]

def open_service_window():
    print("open_service_window called!")  # Debugging
    name = name_entry.get()
    if not name:
        messagebox.showerror("Error", "Name cannot be empty, please enter your name!")
        return

    root.withdraw()
    try:
        print(services_content)  # Debugging
        ServiceWindow(root, name, services_content)
    except Exception as e:
        print(f"Error creating ServiceWindow: {e}")
        messagebox.showerror("Error", f"An error occurred: {e}")


for service in services:
    radio_button = tk.Radiobutton(
        root,
        text=service,
        variable=service_var,
        value=service,
        bg="darkgreen",
        fg="white",
    )
    radio_button.pack(anchor=tk.W)

tk.Button(
    root, text="Submit", command=open_service_window, bg="white", fg="black"
).pack(pady=10)

# Run the main application loop
root.mainloop()
