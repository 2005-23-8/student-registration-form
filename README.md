# student-registration-form
import tkinter as tk
from tkinter import messagebox
from fpdf import FPDF

class DataEntryApp:
    def _init_(self, master):
        self.master = master
        self.master.title("Data Entry App")

        # Labels and Entry fields
        self.label_name = tk.Label(master, text="Name:")
        self.label_name.grid(row=0, column=0, sticky="w")
        self.entry_name = tk.Entry(master)
        self.entry_name.grid(row=0, column=1)

        self.label_age = tk.Label(master, text="Age:")
        self.label_age.grid(row=1, column=0, sticky="w")
        self.entry_age = tk.Entry(master)
        self.entry_age.grid(row=1, column=1)

        # Button to submit data
        self.submit_button = tk.Button(master, text="Submit", command=self.submit_data)
        self.submit_button.grid(row=2, columnspan=2)

    def submit_data(self):
        name = self.entry_name.get()
        age = self.entry_age.get()

        # Data validation
        if not name:
            messagebox.showerror("Error", "Name cannot be empty")
            return
        if not age.isdigit():
            messagebox.showerror("Error", "Age must be a number")
            return

        # Generate PDF
        self.generate_pdf(name, age)
        messagebox.showinfo("Success", "PDF generated successfully")

    def generate_pdf(self, name, age):
        pdf = FPDF()
        pdf.add_page()
        pdf.set_font("Arial", size=12)
        pdf.cell(200, 10, txt="Data Entry Form", ln=True, align="C")
        pdf.cell(200, 10, txt="", ln=True)  # Empty line

        # Adding data to PDF
        pdf.cell(200, 10, txt=f"Name: {name}", ln=True)
        pdf.cell(200, 10, txt=f"Age: {age}", ln=True)

        # Save PDF
        pdf.output("data_entry_form.pdf")

def main():
    root = tk.Tk()
    app = DataEntryApp(root)
    root.mainloop()

if _name_ == "_main_":
    main()
