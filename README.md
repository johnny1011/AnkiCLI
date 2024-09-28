# Anki-like CLI Flashcard Application


[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/infobp8)

## Description

This is a Python-based command-line interface (CLI) application that functions as a flashcard system, similar to Anki. It allows you to add flashcards, review them using the SM-2 spaced repetition algorithm, and utilizes OpenAI's GPT-4 to grade your answers. The application runs entirely in the terminal, making it lightweight and easy to use.

## Features

- **Add Flashcards**: Quickly add new flashcards with front and back text, along with optional tags for categorization.
- **Review Flashcards**: Review flashcards that are due based on the SM-2 algorithm, ensuring efficient learning.
- **Answer Grading**: Input your answer during reviews and receive immediate feedback graded by OpenAI's GPT-4.
- **Difficulty Rating**: After each review, rate the difficulty of recalling the answer to adjust future review intervals.
- **Statistics Tracking**: View your study progress and flashcard statistics over time.

## Installation

### Prerequisites

- **Python 3.6** or higher.
- **OpenAI API Key**: You need an OpenAI API key with access to the GPT-4 model.

### Clone the Repository

Clone this repository to your local machine using:
```bash
git clone https://github.com/yourusername/ankicli.git
cd ankicli
```

### Set Up a Virtual Environment (Optional but Recommended)

Create and activate a virtual environment to manage dependencies:

```bash
python3 -m venv venv
source venv/bin/activate
```

### Install Dependencies

Install the required Python packages:

```bash
pip install openai python-dotenv
```

### Configure the OpenAI API Key

Create a `.env` file in the project directory:

```bash
touch .env
```

Add your OpenAI API key to the `.env` file:

```
OPENAI_API_KEY=your_api_key_here
```

Replace `your_api_key_here` with your actual OpenAI API key.

### Make the Script Executable

Ensure the `anki` script has execute permissions:

```bash
chmod +x anki
```

### Set Up the `anki` Command Without `sudo`

To run the `anki` command from anywhere without using `sudo`, add the script's directory to your `PATH` environment variable.

#### 1. Edit Your Shell Configuration File

Depending on your shell (`zsh` or `bash`), open the appropriate configuration file:

- **For `zsh` users** (default on macOS Catalina and later):

  ```bash
  nano ~/.zshrc
  ```

- **For `bash` users**:

  ```bash
  nano ~/.bash_profile
  ```

#### 2. Add the Script's Directory to `PATH`

Add the following line at the end of the file:

```bash
export PATH="/path/to/ankicli:$PATH"
```

Replace `/path/to/ankicli` with the actual path to your `ankicli` directory.

#### 3. Reload Your Shell Configuration

Apply the changes by reloading your shell configuration:

- **For `zsh` users**:

  ```bash
  source ~/.zshrc
  ```

- **For `bash` users**:

  ```bash
  source ~/.bash_profile
  ```

#### 4. Ensure the Script Is Executable

Make sure the `anki` script is executable:

```bash
chmod +x /path/to/ankicli/anki
```

#### 5. Verify the Setup

Test that the `anki` command is recognized:

```bash
anki --help
```

You should see the help message for the `anki` command. If you encounter any errors, double-check the steps above.

## Usage

### Adding a Flashcard

Add a new flashcard using the `add` command with the `--front` and `--back` options. You can also add tags using `--tags`.

**Example:**

```bash
anki add --front "What is the capital of France?" --back "Paris" --tags "geography,Europe"
```

**Using Shorthand Flags:**

```bash
anki add -f "What is the capital of France?" -b "Paris" -t "geography,Europe"
```

### Reviewing Flashcards

Review due flashcards using the `review` command:

```bash
anki review
```

**Review Process:**

- The application displays the front text of the flashcard.
- You input your answer.
- GPT-4 grades your answer and provides feedback.
- The correct answer is displayed.
- You rate your recall as `easy`, `medium`, or `hard`.
- The flashcard's review interval is updated based on your rating.

### Viewing Statistics

View your study statistics using the `stats` command:

```bash
anki stats
```

This displays:

- Total number of flashcards.
- Number of flashcards due today.
- Average easiness factor.

## Example Session

### 1. Adding Flashcards

```bash
anki add -f "What is the process by which plants make their food?" -b "Photosynthesis" -t "biology,plants"
anki add -f "Who wrote 'To Kill a Mockingbird'?" -b "Harper Lee" -t "literature,authors"
```

### 2. Reviewing Flashcards

```bash
anki review
```

**Sample Output:**

```
Front: What is the process by which plants make their food?
Your answer: Photosynthesis

GPT-4 Assessment: Correct! Plants make their food through photosynthesis.

Correct Answer: Photosynthesis
Rate your recall ('easy', 'medium', 'hard'): easy
Next review in 6 day(s).

Front: Who wrote 'To Kill a Mockingbird'?
Your answer: J.K. Rowling

GPT-4 Assessment: Incorrect. The correct author is Harper Lee, not J.K. Rowling.

Correct Answer: Harper Lee
Rate your recall ('easy', 'medium', 'hard'): hard
Next review in 1 day(s).

Review session complete.
```

### 3. Viewing Statistics

```bash
anki stats
```

**Sample Output:**

```
Total flashcards: 2
Flashcards due today: 0
Average Easiness Factor: 2.55
```

## Data Storage

- **Flashcards File**: The flashcards are stored in a file named `flashcards.json` in the project directory.
- **Backup**: Regularly back up `flashcards.json` to prevent data loss.
- **Manual Editing**: Avoid manually editing `flashcards.json` to prevent data corruption.

## Dependencies

- **openai**: For interacting with the OpenAI API.
- **python-dotenv**: For loading environment variables from the `.env` file.

Install all dependencies using:

```bash
pip install -r requirements.txt
```

*Alternatively, install individually:*

```bash
pip install openai python-dotenv
```

## Notes

- **API Usage and Costs**: Using the OpenAI API incurs costs based on usage. Monitor your API usage on the OpenAI dashboard to manage expenses.
- **Model Access**: Ensure your OpenAI API key has access to the GPT-4 model. If not, you can modify the script to use `gpt-3.5-turbo` in the `grade_answer` function.
- **Data Privacy**: Your answers and the correct answers are sent to OpenAI's servers for processing. Be mindful of any sensitive information.

## Troubleshooting

- **`anki` Command Not Found**: Ensure that the script's directory is correctly added to your `PATH` and that the script is executable.
- **OpenAI API Errors**: Double-check your API key in the `.env` file and ensure you have internet connectivity.
- **Permission Denied**: If you receive a permission error, make sure the script has execute permissions (`chmod +x anki`).

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository.
2. Create a new branch for your feature or bugfix.
3. Commit your changes with clear messages.
4. Open a pull request describing your changes.

## License

This project is licensed under the [MIT License](LICENSE).

## Acknowledgments

- **Anki**: Inspiration for the spaced repetition algorithm and flashcard concept.
- **OpenAI**: Providing the GPT-4 model for answer grading.

---

**Enjoy efficient and intelligent studying with your new CLI flashcard application!**
