# PASSWORD-STRENGTH-CHECKER
# Description:  A Python tool that analyzes user-entered passwords and classifies them as Weak, Moderate, or Strong. It checks length, character variety (uppercase, lowercase, numbers, special characters), and # common/guessable passwords. The tool also provides feedback and suggestions to improve weak passwords. 

import re

def check_password_strength(password):
    strength_points = 0
    feedback = []

    # 1. Length Check
    if len(password) >= 12:
        strength_points += 2
    elif len(password) >= 8:
        strength_points += 1
    else:
        feedback.append("Password is too short (use at least 8 characters).")

    # 2. Uppercase Letters
    if re.search(r"[A-Z]", password):
        strength_points += 1
    else:
        feedback.append("Add at least one uppercase letter.")

    # 3. Lowercase Letters
    if re.search(r"[a-z]", password):
        strength_points += 1
    else:
        feedback.append("Add at least one lowercase letter.")

    # 4. Numbers
    if re.search(r"[0-9]", password):
        strength_points += 1
    else:
        feedback.append("Add at least one number.")

    # 5. Special Characters
    if re.search(r"[!@#$%^&*(),.?\":{}|<>]", password):
        strength_points += 2
    else:
        feedback.append("Add at least one special character (!@#$ etc.).")

    # 6. No spaces
    if " " in password:
        feedback.append("Avoid spaces in password.")

    # 7. Common Passwords Check (basic list, can be expanded)
    common_passwords = ["password", "123456", "qwerty", "abc123", "admin", "letmein"]
    if password.lower() in common_passwords:
        feedback.append("This password is too common and easy to guess.")
        strength_points = 0  # force weak

    # Strength Assessment
    if strength_points >= 7:
        strength = "Strong ✅"
    elif 4 <= strength_points < 7:
        strength = "Moderate ⚠️"
    else:
        strength = "Weak ❌"

    return strength, feedback


# ----------- Run Program ------------
if __name__ == "__main__":
    print("==== Password Strength Checker ====")
    user_password = input("Enter your password: ").strip()
    strength, feedback = check_password_strength(user_password)

    print(f"\nPassword Strength: {strength}")
    if feedback:
        print("Suggestions to improve:")
        for f in feedback:
            print(" -", f)
    else:
        print("Your password looks great!")

