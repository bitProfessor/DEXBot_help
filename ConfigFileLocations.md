有时，您可以通过重新启动来解决问题，也就是删除保存密钥和配置的文件。
# Windows
## DEXBot
- DEXBot config: C:\Users\<user>\AppData\Local\Codaone Oy\dexbot\config.yml
- DEXBot log: C:\Users\<user>\AppData\Local\Codaone Oy\dexbot\dexbot.log
- DEXBot storage: C:\Users\<user>\AppData\Local\Codaone Oy\dexbot\dexbot.sqlite
- Orders history: C:\Users\<user>\AppData\Local\Codaone Oy\dexbot\history.csv
- Uptick
Wallet: C:\Users\<user>\AppData\Local\Fabian Schuh\bitshares\bitshares.sqlite
# Linux
## DEXBot
- DEXBot config: ~/.config/dexbot/config.yml
- DEXBot log: dexbot.log in working directory (the dir within which you started dexbot) for cli version, and ~/.local/share/dexbot/dexbot.log for the GUI version
- DEXBot storage: ~/.local/share/dexbot/dexbot.sqlite
- Orders history: ~/.local/share/dexbot/history.csv
- Uptick
Wallet: ~/.local/share/bitshares/bitshares.sqlite
# OSX
## DEXBot
- DEXBot log: dexbot.log in the same repository as Makefile
- DEXBot config: ~/Library/Application Support/dexbot/config.yml
- DEXBot log: dexbot.log in the working directory (if you start dexbot from cli)
- DEXBot storage: ~/Library/Application Support/dexbot/dexbot.sqlite
- Orders history: ~/Library/Application Support/dexbot/orders.csv
# Uptick
Wallet: ~/Library/Application Support/bitshares/bitshares.sqlite