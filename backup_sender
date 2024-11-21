import tkinter as tk
from tkinter import filedialog
import os
import json
import requests

settings_file = "settings.json"

def path(settings_file):
    if os.path.exists(settings_file):
        try:
            with open(settings_file, "r") as file:
                data = json.load(file)
                saved_path = data.get("folder_path", "")
                print(f"Folder path is: {saved_path}")
        except Exception as e:
            print(f"Error reading settings file: {e}")
            saved_path = ""
    else:
        root = tk.Tk()
        root.withdraw()
        print("chose youre backup folder:")
        folder_path = filedialog.askdirectory(title="Select a Folder")

        if folder_path:
            try:
                with open(settings_file, "w") as file:
                    json.dump({"folder_path": folder_path}, file)
                saved_path = folder_path
                print(f"Folder path saved: {folder_path}")
            except Exception as e:
                print(f"Error saving settings file: {e}")
                saved_path = ""
        else:
            print("No folder selected.")
            saved_path = ""

    return saved_path


backup_folder_path = path(settings_file)

telegram_bot_token = 'XXXXXXX'
chat_id = 'XXXXXXX'


def send_file_to_telegram(file_path):
    if not os.path.exists(file_path):
        print(f"File does not exist: {file_path}")
        return

    with open(file_path, 'rb') as file:
        url = f'https://api.telegram.org/bot{telegram_bot_token}/sendDocument'
        payload = {'chat_id': chat_id}
        files = {'document': file}
        print("sending...")
        try:
            response = requests.post(url, data=payload, files=files)
            if response.status_code == 200:
                print(f'File {file_path} sent successfully!')
            else:
                print(f'Failed to send {file_path}:', response.text)
        except requests.exceptions.RequestException as e:
            print(f"Error sending file: {e}")


def send_latest_backup_file(backup_folder_path):
    if not backup_folder_path:
        print("No folder path provided.")
        return

    files = [f for f in os.listdir(backup_folder_path) if os.path.isfile(os.path.join(backup_folder_path, f))]
    
    if files:
        latest_file = max(files, key=lambda f: os.path.getctime(os.path.join(backup_folder_path, f)))
        latest_file_path = os.path.join(backup_folder_path, latest_file)
        print(f"file is: {latest_file}")
        send_file_to_telegram(latest_file_path)
    else:
        print("No files found in the directory.")


send_latest_backup_file(backup_folder_path)
input("Press Enter to exit...")
