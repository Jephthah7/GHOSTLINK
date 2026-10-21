👻 GhostLink

A lightweight, terminal-based private chat prototype for Kali Linux and other Linux systems.

GhostLink is designed around temporary chat sessions, single-use invitations, and automatic session expiration.

✨ Features
🖥️ Terminal-based interface.
🔗 Invitation links for joining a chat.
🔒 Authenticated message encryption using PyNaCl.
⏱️ Configurable session duration.
🗑️ Terminal display refreshes every 50 seconds.
🚪 End a session manually.
♻️ Invitations are designed for single use.
💾 No intentional conversation transcript storage.
⚠️ Important Security Notice

GhostLink is an experimental prototype, not a production-ready secure messaging application.

The relay must be reachable by both participants.
The prototype relay uses plain TCP, not TLS.
The invitation contains the chat encryption key. Anyone who obtains the complete invitation may be able to join or compromise the intended session, depending on its state.
Clearing the terminal does not securely erase messages from memory, terminal scrollback, screenshots, backups, or other system artifacts.
The application cannot guarantee that all traces of a conversation are erased.
The current prototype has not undergone an independent security audit.
Do not use it to exchange passwords, financial information, or other highly sensitive data.

Use GhostLink only with people who have agreed to participate.

📋 Requirements

You need:

Kali Linux or another compatible Linux distribution.
Python 3.
Git (optional, for cloning the repository).
Internet or network access between the participants and the relay server.
Permission to run the relay server on the machine hosting it.
🛠️ Installation on Kali Linux
Step 1: Update your package lists

Open a terminal and run:

sudo apt update
Step 2: Install the required system packages
sudo apt install -y python3 python3-venv python3-pip git
Step 3: Download GhostLink

If you have Git installed, clone this repository:

git clone https://github.com/jephthah7/ghostlink.git

Replace YOUR-USERNAME with your actual GitHub username.

Enter the project directory:

cd ghostlink

Alternative: Download the repository as a ZIP from GitHub, extract it, open a terminal inside the extracted ghostlink directory, and continue to the next step.

Step 4: Create a Python virtual environment
python3 -m venv .venv

Activate it:

source .venv/bin/activate
Step 5: Install the Python dependency
python -m pip install --upgrade pip
python -m pip install -r requirements.txt

This installs the Python dependencies listed by the project, including PyNaCl.

Step 6: Check the Python files
python -m py_compile ghostlink.py relay.py

If the command returns without an error, the files pass Python's syntax check.

🌐 Running the Relay Server

The relay forwards messages between the two participants. Both participants must be able to reach the relay.

On the machine that will host the relay, open a terminal inside the GhostLink directory and activate the virtual environment:

source .venv/bin/activate

Start the relay:

python relay.py

Keep this terminal open while the session is running.

Networking note: Before connecting from another machine, verify the relay's listening address and port in relay.py. Configure your firewall and network only as necessary for your own test environment. Do not expose an unencrypted relay to the public internet and assume the connection is secure.

💬 Using GhostLink

The exact commands and options depend on the current implementation of ghostlink.py. Check its built-in help before starting:

python ghostlink.py --help

If the script does not provide a help screen, inspect the usage section near the bottom of ghostlink.py before running it.

Starting a session
Start the relay server.
On the host machine, open a second terminal in the project directory.

Activate the virtual environment:

source .venv/bin/activate
Run the host command supported by the current script.
Choose the session duration if the program prompts for it, or use the duration option documented by the script.
Share the generated invitation with the intended participant through a private channel.
Joining a session
Install GhostLink on the joining machine using the installation steps above.
Make sure that machine can reach the relay.
Activate the virtual environment.
Run the join command supported by the current script.
Enter or paste the invitation when prompted.

Never post a live invitation in a public issue, public chat, or repository. Treat it as a secret.

Ending a session

Use the application's supported exit command to end the conversation. The prototype is intended to expire sessions after the configured duration and invalidate used invitations.

Do not assume that ending a session securely deletes every copy of a message or every trace left on either computer.

🧪 Running the Tests

From the project directory, activate the virtual environment and run:

python -m unittest discover -s tests -v

The tests cover selected prototype functionality. Passing these tests does not establish that the application is secure or production-ready.

📁 Project Structure
ghostlink/
├── ghostlink.py
├── relay.py
├── requirements.txt
├── README.md
├── LICENSE
├── .gitignore
└── tests/
    └── test_sessions.py
🔐 Security and Privacy

GhostLink aims to minimize intentional message retention, but it does not promise zero traces.

Potential traces include:

Terminal scrollback and screenshots.
Process memory and operating-system swap.
System logs and crash reports.
Network metadata.
Copies of invitations or messages saved by participants.

Review the source code before using the application and do not rely on this prototype for high-risk communications.

🤝 Contributing

Contributions, bug reports, and security reviews are welcome.

When reporting a problem, do not include active invitation links, encryption keys, or private conversation content.

📜 License

This project is distributed under the license included in the repository. See LICENSE for details.
