import random
import string
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Adjectives and Nouns for username generation
adjectives = ["Happy", "Cool", "Sneaky", "Brave", "Funky", "Witty", "Wild", "Lucky", "Silly", "Angry"]
nouns = ["Tiger", "Dragon", "Panda", "Knight", "Ninja", "Eagle", "Wizard", "Lion", "Wolf", "Robot"]

# Track generation stats using pandas
username_data = pd.DataFrame(columns=["Username", "Adjective", "Noun", "NumberIncluded", "SpecialIncluded", "Length"])

# Function to generate a username
def generate_username(include_number=True, include_special=True, length=None):
    adj = np.random.choice(adjectives)
    noun = np.random.choice(nouns)
    username = adj + noun

    if include_number:
        num = str(np.random.randint(0, 999))
        username += num
    else:
        num = ''

    if include_special:
        special = random.choice("!@#$%^&*")
        username += special
    else:
        special = ''

    if length:
        username = username[:length]

    # Save info to DataFrame
    global username_data
    username_data = pd.concat([
        username_data,
        pd.DataFrame([{
            "Username": username,
            "Adjective": adj,
            "Noun": noun,
            "NumberIncluded": bool(num),
            "SpecialIncluded": bool(special),
            "Length": len(username)
        }])
    ], ignore_index=True)

    return username

# Save usernames to file
def save_to_file(df, filename="usernames.txt"):
    try:
        df['Username'].to_csv(filename, index=False, header=False)
        print(f"\n Saved {len(df)} usernames to '{filename}'")
    except Exception as e:
        print(f"❌ Error saving to file: {e}")

# Visualize data using matplotlib
def plot_stats(df):
    plt.figure(figsize=(10, 5))

    # Count of adjectives and nouns used
    plt.subplot(1, 2, 1)
    df['Adjective'].value_counts().plot(kind='bar', color='skyblue')
    plt.title("Adjective Frequency")
    plt.xticks(rotation=45)

    plt.subplot(1, 2, 2)
    df['Noun'].value_counts().plot(kind='bar', color='lightgreen')
    plt.title("Noun Frequency")
    plt.xticks(rotation=45)

    plt.tight_layout()
    plt.show()

# Main function
def main():
    print(" RANDOM USERNAME GENERATOR \n")
    try:
        count = int(input("How many usernames to generate? "))
        use_number = input("Include numbers? (yes/no): ").lower().startswith("y")
        use_special = input("Include special characters? (yes/no): ").lower().startswith("y")
        use_length = input("Limit username length? (yes/no): ").lower().startswith("y")

        length = None
        if use_length:
            length = int(input("Enter maximum length of username: "))

        print("\n Generated Usernames:\n")
        for _ in range(count):
            print("→", generate_username(use_number, use_special, length))

        # Save and plot
        save_to_file(username_data)
        plot_stats(username_data)

    except Exception as e:
        print(f" Error: {e}")

if __name__ == "_main_":
    main()
