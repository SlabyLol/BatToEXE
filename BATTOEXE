import tkinter as tk
from tkinter import filedialog, messagebox
import subprocess
import os

def select_bat():
    path = filedialog.askopenfilename(filetypes=[("Batch files", "*.bat")])
    if path:
        bat_entry.delete(0, tk.END)
        bat_entry.insert(0, path)

def select_output():
    path = filedialog.askdirectory()
    if path:
        output_entry.delete(0, tk.END)
        output_entry.insert(0, path)

def convert():
    bat_path = bat_entry.get()
    output_dir = output_entry.get()
    
    if not os.path.isfile(bat_path):
        messagebox.showerror("Error", "The selected BAT file does not exist!")
        return
    if not os.path.isdir(output_dir):
        messagebox.showerror("Error", "The output folder is invalid!")
        return
    
    try:
        # Command to run PyInstaller
        cmd = [
            "pyinstaller",
            "--onefile",   # create a single EXE
            "--distpath", output_dir,
            bat_path
        ]
        subprocess.run(cmd, check=True)
        messagebox.showinfo("Success", f"EXE has been created in:\n{output_dir}")
    except subprocess.CalledProcessError as e:
        messagebox.showerror("Error", f"Conversion failed:\n{e}")

# Tkinter GUI
root = tk.Tk()
root.title("BAT to EXE Converter Copyright by DarkFox Co.")

tk.Label(root, text="BAT file:").grid(row=0, column=0, padx=5, pady=5)
bat_entry = tk.Entry(root, width=50)
bat_entry.grid(row=0, column=1, padx=5, pady=5)
tk.Button(root, text="Browse", command=select_bat).grid(row=0, column=2, padx=5, pady=5)

tk.Label(root, text="Output folder:").grid(row=1, column=0, padx=5, pady=5)
output_entry = tk.Entry(root, width=50)
output_entry.grid(row=1, column=1, padx=5, pady=5)
tk.Button(root, text="Browse", command=select_output).grid(row=1, column=2, padx=5, pady=5)

tk.Button(root, text="Convert", command=convert, width=20, bg="green", fg="white").grid(row=2, column=0, columnspan=3, pady=20)

root.mainloop()
