import tkinter as tk
from tkinter import messagebox
from PIL import Image, ImageTk

def open_service_window():
    name = name_entry.get()
    if not name:
        messagebox.showerror("Error", "Name cannot be empty; please type: Advanced Facials, Permanent Jewelry, Body Waxing, Swedish Massages or Spray Tans to learn more info.")
        return

    root.withdraw()
    ServiceWindow(root, name)

def close_app():
    root.destroy()

class ServiceWindow:
    def __init__(self, master, name):
        self.master = master
        self.window = tk.Toplevel(master)
        self.window.title("Select a Selfcare Service")

        tk.Label(self.window, text=f"Welcome, {name}!").pack(pady=10)

        self.service_var = tk.StringVar(value="Facial")
        services = ["Advanced Facials", "Permanent Jewelry", "Swedish Massages", "Spray Tans", "Body Waxing"]
        for service in services:
            tk.Radiobutton(self.window, text=service, variable=self.service_var, value=service).pack(anchor=tk.W)

        img_path = "C:/Users/Ginny/Downloads/images/IMG_9398.jpeg"
        img = Image.open(img_path)  
        self.advanced_facial_img = ImageTk.PhotoImage(img)
        tk.Label(self.window, image=self.advanced_facial_img, text="Advanced Facials", compound="bottom").pack(pady=10)

        img_path = "C:/Users/Ginny/Downloads/images/IMG_3670.jpeg"
        img2 = Image.open(img_path) 
        self.permanent_jewelry_img = ImageTk.PhotoImage(img2)
        tk.Label(self.window, image=self.permanent_jewelry_img, text="Permanent Jewelry", compound="bottom").pack(pady=10)

        img_path = "C:/Users/Ginny/Downloads/images/IMG_2641.jpeg"
        img3 = Image.open(img_path) 
        self.body_waxing_img = ImageTk.PhotoImage(img3)
        tk.Label(self.window, image=self.body_waxing_img, text="Body Waxing", compound="bottom").pack(pady=10)

        tk.Button(self.window, text="Submit", command=self.submit).pack(pady=10)
        tk.Button(self.window, text="Back", command=self.go_back).pack(pady=5)

    def submit(self):
        selected_service = self.service_var.get()
        messagebox.showinfo("Service Selected", f"You have selected {selected_service}.")

    def go_back(self):
        self.window.destroy()
        self.master.deiconify()

# Define the content for each service
services_content = {
    "Advanced Facials": "Advanced Facials include customized treatments that target specific skin concerns and include; double cleanses, exfoliation, extractions, facial massage, mask treatment with scalp, shoulder or hand massage, Celluma LED Therapy, serums, lip treatment, moisturizer and SPF. Prep; come in without makeup on and let your Esti know if you have any med or skincare changes. Aftercare; discontinue serums for 2 days, use SPF daily.",
    "Permanent Jewelry": "Permanent Jewelry involves custom-fitted 14K Gold Filled, Sterling Silver and Enamel bracelets, anklets and necklaces that are welded shut using a small welder with argon gas. If you need to break the chain for a medical procedure, cut the chain at the jump ring and bring it back in for a free re-weld.",
    "Body Waxing": "Body Waxing provides smooth and hair-free skin for 2-6 weeks. It is recommended to let hair grow 1/2 inch, exfoliate 2-3X per week, moisturize daily with pure aloe and rebook in 4-6 weeks for maintenance.",
    "Swedish Massages": "Swedish massages involve long, fluid strokes of muscles and tissues with a focus on relaxation and helping alleviate muscle tension.",
    "Spray Tans": "Spray Tans give you a natural-looking, sun-kissed glow without the UV exposure and can last 7-10 days with proper aftercare. Prep the skin by exfoliating and moisturizing days before your tan. The day of your tan; come in with loose clothes, no makeup, deoderant or lotion on. Aftercare; wait 5-12HRS to rinse, pat yourself dry and moisturize daily."
}

root = tk.Tk()
root.title("Ginny Rose Studio: Skincare Services")

tk.Label(root, text="Welcome, please view the information about the selfcare services I offer in my studio!").pack(pady=10)
tk.Label(root, text="Name").pack()
name_entry = tk.Entry(root)
name_entry.pack()

tk.Label(root, text="Permanent Jewelry").pack()
tk.Label(root, text="Body Waxing").pack()
tk.Label(root, text="Advanced Facials").pack()
tk.Label(root, text="Spray Tans").pack()
tk.Label(root, text="Swedish Massages").pack()

tk.Label(root, text="Select a Service").pack()
service_var = tk.StringVar(value="Facial")
services = ["Advanced Facials", "Permanent Jewelry", "Swedish Massages", "Spray Tans", "Body Waxing"]
for service in services:
    radio_button = tk.Radiobutton(root, text=service, variable=service_var, value=service)
    radio_button.pack(anchor=tk.W)
    radio_button.bind("<Button-1>", lambda event, svc=service: open_service_window())

tk.Button(root, text="Next", command=open_service_window).pack(pady=10)
tk.Button(root, text="Exit", command=close_app).pack(pady=5)

root.mainloop()
