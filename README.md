
# Backup File Sender to Telegram

### This Python application helps you automatically send backup files from a designated folder to a Telegram chat using a Telegram bot. It simplifies the process of monitoring and sending important backup files without requiring manual intervention.

#### Features   :)
1. Folder Selection: The program prompts you to select a folder the first time you run it, and automatically saves the path for future use.
2. Automatic File Selection: It identifies the latest file in the selected folder based on creation time and sends it to your Telegram chat.
3. Telegram Integration: Using a Telegram bot, the program sends files directly to a specified chat.
4. Easy Configuration: After the first setup, the program doesn't ask for the folder path again your settings are saved in a JSON file.


#### Requirements:

1. Python `3.x`
2. `requests` library (can be installed via `pip install requests`)
3. A Telegram bot (you can create one via [@BotFather](https://t.me/BotFather)) and a chat ID to receive the files.

### Configure the Bot:
Open the script and replace the `telegram_bot_token` and `chat_id` variables with your own values:

```python
telegram_bot_token = 'your_bot_token'
chat_id = 'your_chat_id'
```

### Run the Script:
Run the Python script using your terminal:
```bash
python app.py
```

The program will ask you to select the folder containing the backup files. After the first run, it will remember the folder path.
