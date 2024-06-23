import tkinter as tk
from time import time


sample_text = "i have to go home"


def start_test():
    global start_time
    start_time = time()
    entry.delete(0, tk.END)
    entry.config(state=tk.NORMAL)
    entry.focus()


def end_test(event):
    end_time = time()
    elapsed_time = end_time - start_time
    typed_text = entry.get()
    
   
    words = len(typed_text.split())
    wpm = (words / elapsed_time) * 60
    
    
    correct_chars = sum(1 for i, c in enumerate(typed_text) if i < len(sample_text) and c == sample_text[i])
    accuracy = (correct_chars / len(sample_text)) * 100

    
    result_label.config(text=f"WPM: {wpm:.2f}\nAccuracy: {accuracy:.2f}%")
    entry.config(state=tk.DISABLED)


root = tk.Tk()
root.title("Typing Speed Calculator")


sample_label = tk.Label(root, text=sample_text, wraplength=400, justify="center")
sample_label.pack(pady=10)


entry = tk.Entry(root, width=50, state=tk.DISABLED)
entry.pack(pady=10)
entry.bind("<Return>", end_test)


start_button = tk.Button(root, text="Start", command=start_test)
start_button.pack(pady=10)


result_label = tk.Label(root, text="", wraplength=400, justify="center")
result_label.pack(pady=10)


root.mainloop()
