import tkinter as tk

def click(event):
    global expression
    text = event.widget.cget("text")
    if text == "=":
        try:
            result = str(eval(expression))
            display_var.set(result)
            expression = result
        except Exception as e:
            display_var.set("Error")
            expression = ""
    elif text == "C":
        expression = ""
        display_var.set("")
    else:
        expression += text
        display_var.set(expression)

root = tk.Tk()
root.geometry("300x400")
root.title("Python Calculator")

expression = ""
display_var = tk.StringVar()

# Display Entry
entry = tk.Entry(root, textvar=display_var, font="Arial 20", justify="right")
entry.pack(fill="both", ipadx=8, pady=10)

# Button Frame
btn_frame = tk.Frame(root)
btn_frame.pack()

# Button layout
buttons = [
    ["7", "8", "9", "/"],
    ["4", "5", "6", "*"],
    ["1", "2", "3", "-"],
    ["0", ".", "=", "+"],
    ["C"]
]

for row in buttons:
    row_frame = tk.Frame(btn_frame)
    row_frame.pack(expand=True, fill="both")
    for btn_text in row:
        btn = tk.Button(row_frame, text=btn_text, font="Arial 18", relief="ridge", border=1)
        btn.pack(side="left", expand=True, fill="both")
        btn.bind("<Button-1>", click)

root.mainloop()
