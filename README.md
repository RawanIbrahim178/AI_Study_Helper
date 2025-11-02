# AI_Study_Helper
An AI-powered tool that summarizes and simplifies study materials to help students learn faster.
from transformers import pipeline

def summarize_text(text):
    summarizer = pipeline("summarization", model="facebook/bart-large-cnn")
    summary = summarizer(text, max_length=80, min_length=30, do_sample=False)
    return summary[0]['summary_text']

if __name__ == "__main__":
    print("📚 Welcome to AI Study Helper!")
    print("Paste a paragraph (or multiple) and press Enter. Type 'EXIT' to quit.\n")
    while True:
        text = input("Enter text (or type EXIT):\n")
        if text.strip().upper() == "EXIT":
            print("Goodbye! 👋")
            break
        if len(text.strip()) < 10:
            print("Please enter a longer paragraph to summarize.\n")
            continue
        try:
            summary = summarize_text(text)
            print("\n🧠 Summary:")
            print(summary + "\n")
        except Exception as e:
            print("Error (maybe model not downloaded or no internet):", e)
            print("You can also run this in Google Colab if your device can't install the model.\n")
