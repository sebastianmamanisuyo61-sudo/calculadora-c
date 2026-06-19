# calculadora-c
calculadora generada con inteligencia artificial basándose en una calculadora científica.
import tkinter as tk
from tkinter import ttk
import math

# --- Configuración de Estilos ---
COLORS = {
    "bg": "#2c3e50",
    "screen": "#34495e",
    "text": "#ecf0f1",
    "btn_num": "#7f8c8d",
    "btn_op": "#e67e22",
    "btn_equal": "#27ae60"
}

def create_calculator():
    root = tk.Tk()
    root.title("Calculadora Científica")
    root.geometry("350x500")
    root.configure(bg=COLORS["bg"])

    # Pantalla
    screen = tk.Entry(root, font=("Arial", 24), borderwidth=0, 
                      bg=COLORS["screen"], fg=COLORS["text"], justify='right')
    screen.grid(row=0, column=0, columnspan=4, padx=10, pady=20, sticky="nsew")

    def press(key):
        if key == "=":
            try:
                result = eval(screen.get())
                screen.delete(0, tk.END)
                screen.insert(tk.END, str(result))
            except:
                screen.delete(0, tk.END)
                screen.insert(tk.END, "Error")
        elif key == "C":
            screen.delete(0, tk.END)
        else:
            screen.insert(tk.END, key)

    # Botones
    buttons = [
        '7', '8', '9', '/',
        '4', '5', '6', '*',
        '1', '2', '3', '-',
        'C', '0', '=', '+'
    ]

    row_val = 1
    col_val = 0
    for button in buttons:
        action = lambda x=button: press(x)
        bg_color = COLORS["btn_num"]
        if button in ['/', '*', '-', '+']: bg_color = COLORS["btn_op"]
        if button == '=': bg_color = COLORS["btn_equal"]
        
        tk.Button(root, text=button, width=5, height=2, font=("Arial", 14, "bold"),
                  bg=bg_color, fg="white", command=action).grid(row=row_val, column=col_val, padx=5, pady=5, sticky="nsew")
        
        col_val += 1
        if col_val > 3:
            col_val = 0
            row_val += 1

    root.mainloop()

if __name__ == "__main__":
    create_calculator()
