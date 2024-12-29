import tkinter as tk
from tkinter import messagebox

class CurrencyConverterApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Currency Converter")

        self.exchange_rates = {
            "USD": 1.0,
            "EUR": 0.85,
            "INR": 74.5
        }

        tk.Label(root, text="Amount:").grid(row=0, column=0)
        self.amount_entry = tk.Entry(root)
        self.amount_entry.grid(row=0, column=1)

        tk.Label(root, text="From Currency:").grid(row=1, column=0)
        self.from_currency = tk.StringVar(value="USD")
        tk.OptionMenu(root, self.from_currency, *self.exchange_rates.keys()).grid(row=1, column=1)

        tk.Label(root, text="To Currency:").grid(row=2, column=0)
        self.to_currency = tk.StringVar(value="EUR")
        tk.OptionMenu(root, self.to_currency, *self.exchange_rates.keys()).grid(row=2, column=1)

        tk.Button(root, text="Convert", command=self.convert).grid(row=3, column=0, columnspan=2)
        self.result_label = tk.Label(root, text="Result: ")
        self.result_label.grid(row=4, column=0, columnspan=2)

    def convert(self):
        try:
            amount = float(self.amount_entry.get())
            from_curr = self.from_currency.get()
            to_curr = self.to_currency.get()

            if from_curr not in self.exchange_rates or to_curr not in self.exchange_rates:
                raise ValueError("Unsupported currency")
            base_amount = amount / self.exchange_rates[from_curr]
            converted_amount = base_amount * self.exchange_rates[to_curr]

            self.result_label.config(text=f"Result: {round(converted_amount, 2)} {to_curr}")
        except ValueError:
            messagebox.showerror("Error", "Invalid input. Please enter a numeric amount.")

if __name__ == "__main__":
    root = tk.Tk()
    app = CurrencyConverterApp(root)
    root.mainloop()
