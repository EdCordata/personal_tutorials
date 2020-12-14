# Python 2 Executable


#### Windows
1) Install [Python & pip](https://www.python.org/downloads/)
2) Build python script to exe:
    ```bash
    pip install pyinstaller
    pyinstaller --onefile example.py
    ```


#### Linux
1) Install Python & pip
    ```bash
    sudo apt install -y python3
    sudo apt install -y python3-pip
    ```
2) Build python script to executable:
    ```bash
    pip3 install pyinstaller
    python3 -m PyInstaller --onefile example.py
    ```
