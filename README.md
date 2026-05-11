import tkinter as tk
import random

# Create window
root = tk.Tk()
root.title("Gift Card")
root.geometry("500x300")
root.configure(bg="#0f172a")

canvas = tk.Canvas(root, width=500, height=300, bg="#0f172a", highlightthickness=0)
canvas.pack()

# Create floating particles
particles = []
for _ in range(30):
    x = random.randint(0, 500)
    y = random.randint(0, 300)
    size = random.randint(2, 5)
    p = canvas.create_oval(x, y, x+size, y+size, fill="#38bdf8", outline="")
    particles.append((p, random.uniform(0.5, 2)))

# Text (gift message)
text = canvas.create_text(
    250, 150,
    text="🎁 Surprise 🎁",
    fill="#facc15",
    font=("Helvetica", 24, "bold")
)

subtext = canvas.create_text(
    250, 200,
    text="fuck you 😎",
    fill="#f1f5f9",
    font=("Helvetica", 16)
)

# Animate particles
def animate():
    for p, speed in particles:
        canvas.move(p, 0, speed)
        pos = canvas.coords(p)
        if pos[1] > 300:
            canvas.coords(p, random.randint(0, 500), 0, random.randint(0, 500)+3, 3)
    root.after(30, animate)

# Glow animation for main text
colors = ["#facc15", "#fde047", "#fbbf24", "#facc15"]
i = 0

def glow():
    global i
    canvas.itemconfig(text, fill=colors[i % len(colors)])
    i += 1
    root.after(200, glow)

animate()
glow()

root.mainloop()
