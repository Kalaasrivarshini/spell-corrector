import tkinter as tk
from spellchecker import SpellChecker

class SpellCorrectorApp:
    def __init__(self, master):
        self.master = master
        self.master.title("Spell Corrector")

        # Create widgets
        self.label = tk.Label(master, text="Enter text:")
        self.label.pack()

        self.text_entry = tk.Entry(master, width=50)
        self.text_entry.pack()

        self.correct_button = tk.Button(master, text="Correct Spelling", command=self.correct_spelling)
        self.correct_button.pack()

        self.result_label = tk.Label(master, text="")
        self.result_label.pack()

    def correct_spelling(self):
        text_to_check = self.text_entry.get()

        # Use SpellChecker from pyspellchecker library
        spell = SpellChecker()
        misspelled_words = spell.unknown(text_to_check.split())

        # Correct spelling
        corrected_text = " "
        for word in text_to_check.split():
            if word in misspelled_words:
                corrected_text += spell.correction(word) + " "
            else:
                corrected_text += word + " " 

        self.result_label.config(text="Corrected Text: " + corrected_text)

if __name__ == "__main__":
    root = tk.Tk()
    app = SpellCorrectorApp(root)
    root.mainloop()
