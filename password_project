import customtkinter as ctk
import re
import threading
import time

# PASSWORD STRENGTH LOGIC

COMMON_PASSWORDS = {
    "password", "123456", "qwerty", "111111", "admin",
    "iloveyou", "123123", "abc123", "password1", "welcome"
}

def evaluate_password_strength(password: str):
    score = 0
    suggestions = []

    if not password:
        return 0, ["Password cannot be empty."]

    if len(password) >= 12:
        score += 2
    elif len(password) >= 8:
        score += 1
    else:
        suggestions.append("Use at least 8–12 characters.")

    if re.search(r"[A-Z]", password):
        score += 1
    else:
        suggestions.append("Add uppercase letters (A-Z).")

    if re.search(r"[a-z]", password):
        score += 1
    else:
        suggestions.append("Add lowercase letters (a-z).")

    if re.search(r"\d", password):
        score += 1
    else:
        suggestions.append("Add digits (0-9).")

    if re.search(r"[!@#$%^&*(),.?\":{}|<>]", password):
        score += 1
    else:
        suggestions.append("Add special characters (e.g. @ # ? !).")

    if password.lower() in COMMON_PASSWORDS:
        score = max(0, score - 2)
        suggestions.append("Avoid common passwords.")

    if re.search(r"(.)\1{2,}", password):
        suggestions.append("Avoid repeating characters.")

    if password.isdigit():
        suggestions.append("Avoid using only numbers.")

    return score, suggestions

# GUI APP WITH ANIMATIONS

class PasswordStrengthApp(ctk.CTk):
    def __init__(self):
        super().__init__()

        self.title("Premium Password Strength Checker")
        self.geometry("520x420")
        ctk.set_appearance_mode("dark")
        ctk.set_default_color_theme("blue")

        # Title Label
        self.title_label = ctk.CTkLabel(self, text="🔐 Premium Password Checker",
                                        font=("Arial", 24, "bold"),
                                        text_color="cyan")
        self.title_label.pack(pady=15)

        # Input Frame
        input_frame = ctk.CTkFrame(self, fg_color="#222222")
        input_frame.pack(pady=10)

        # Password Entry
        self.password_entry = ctk.CTkEntry(input_frame, 
                                           placeholder_text="Enter your password...",
                                           width=300,
                                           show="*")
        self.password_entry.grid(row=0, column=0, padx=10, pady=10)
        self.password_entry.bind("<KeyRelease>", self.update_strength)

        # Show/Hide Button
        self.show_password = False
        self.toggle_button = ctk.CTkButton(input_frame, text="👁 Show", 
                                           width=70, 
                                           command=self.toggle_password_visibility)
        self.toggle_button.grid(row=0, column=1, padx=5)

        # Progress Bar
        self.strength_bar = ctk.CTkProgressBar(self, width=330)
        self.strength_bar.set(0)
        self.strength_bar.pack(pady=15)

        # Strength Label
        self.strength_label = ctk.CTkLabel(self, text="Strength: ",
                                           font=("Arial", 18, "bold"))
        self.strength_label.pack()

        # Suggestion Label
        self.suggestion_label = ctk.CTkLabel(self, text="",
                                             wraplength=480,
                                             justify="left",
                                             font=("Arial", 14))
        self.suggestion_label.pack(pady=10)

    # Smooth Animation
    def animate_bar(self, target_value):
        current = self.strength_bar.get()
        step = 0.02 if target_value > current else -0.02

        while abs(target_value - current) > 0.01:
            current += step
            self.strength_bar.set(max(0, min(1, current)))
            time.sleep(0.01)

    def toggle_password_visibility(self):
        self.show_password = not self.show_password
        
        if self.show_password:
            self.password_entry.configure(show="")
            self.toggle_button.configure(text="🙈 Hide")
        else:
            self.password_entry.configure(show="*")
            self.toggle_button.configure(text="👁 Show")

    def update_strength(self, event=None):
        password = self.password_entry.get()
        score, suggestions = evaluate_password_strength(password)

        # Calculate bar value
        bar_value = score / 6

        # Run smooth animation in a different thread
        threading.Thread(target=self.animate_bar, args=(bar_value,), daemon=True).start()

        # Color transitions
        if score <= 2:
            color = "red"
            label_text = "Weak"
        elif score <= 4:
            color = "orange"
            label_text = "Medium"
        else:
            color = "lime"
            label_text = "Strong"

        self.strength_bar.configure(progress_color=color)
        self.strength_label.configure(text=f"Strength: {label_text}", text_color=color)

        # Suggestions fade-in effect
        if suggestions:
            final_text = "💡 Suggestions:\n- " + "\n- ".join(suggestions)
            self.suggestion_label.configure(text=final_text, text_color="yellow")
        else:
            self.suggestion_label.configure(text="✅ Your password is strong!",
                                            text_color="lightgreen")

# Run App
if __name__ == "__main__":
    app = PasswordStrengthApp()
    app.mainloop()
