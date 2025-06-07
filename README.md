# guess-number-game
#Importing what we will need
import random
import tkinter as tk


# __our main variables__
number_to_guess = 0
tries_count = 0


def start_new_game():
    global number_to_guess, tries_count # at this line we're saying we trying to change 
    number_to_guess = random.randint(1, 100) # here we will change that
    tries_count = 0 # tries will be reset

    # here we almost reset the window
    instruction_label.config(text="Guess a number between 1,100")
    result_label.config(text="") # here we will delete the result text
    attempts_label.config(text="0 : Try") # at this line we putting tries number on 0
    
    guess_input_box.delete(0, tk.END) # Delete the number in the guess bot
    guess_button.config(state=tk.NORMAL) # activating the buttom guess
    guess_input_box.config(state=tk.NORMAL) # activating the guess input box
    guess_input_box.focus_set() # for better type
# Tries counter function
def check_guess():
    global tries_count
    
    try:
        user_guess = int(guess_input_box.get()) # making an int numb
        
        # if the user wrote a number out of what we told
        if user_guess < 1 or user_guess > 100:
            result_label.config(text="Please enter a number between 1,100")
            return 
        
        # if the number was between 1,100 we will count it by try
        tries_count += 1 
        attempts_label.config(text=f"tries: {tries_count}")
        
        if user_guess > number_to_guess:
            result_label.config(text="your number is lower than your guess")
        elif user_guess < number_to_guess:
            result_label.config(text="your number is higher than your guess")
        else: # یعنی حدس درست بود
            result_label.config(text=f"congrats the number were{number_to_guess} !")
            guess_button.config(state=tk.DISABLED) # now we should disable the buttom and the input box
            guess_input_box.config(state=tk.DISABLED)
# here we are handling the errors           
    except ValueError:
        result_label.config(text="just use number")
        
    guess_input_box.delete(0, tk.END) # after every guess we will empty the box

main_window = tk.Tk() # new window
main_window.title("guess game")
main_window.geometry("300x250") 
main_window.resizable(False, False) # we disabled the user to change the size of the window

# Guide Label
instruction_label = tk.Label(main_window, text="guess a number between 1 , 100", font=("Arial", 10))
instruction_label.pack(pady=5) 

# Box for neww guess
guess_input_box = tk.Entry(main_window, width=20, font=("Arial", 12))
guess_input_box.pack(pady=5)
guess_input_box.focus_set()
guess_input_box.bind("<Return>", lambda event: check_guess()) # if you press the enter it will check

#guess buttom
guess_button = tk.Button(main_window, text="حدس بزن", command=check_guess, font=("Arial", 10))
guess_button.pack(pady=5)

# Label
attempts_label = tk.Label(main_window, text="تلاش‌ها: 0", font=("Arial", 10), fg="purple")
attempts_label.pack(pady=5)

# Label
result_label = tk.Label(main_window, text="", font=("Arial", 10), fg="blue")
result_label.pack(pady=5)

# and buttom for new game 
new_game_button = tk.Button(main_window, text="بازی جدید", command=start_new_game, font=("Arial", 10))
new_game_button.pack(pady=10)
