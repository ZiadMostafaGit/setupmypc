# ❌️ Defender Remover / Defender Disabler

<a href="https://github.com/ionuttbara/windows-defender-remover">
    <picture>
        <source media="(prefers-color-scheme: dark)" srcset="https://github.com/drunkwinter/windows-defender-remover/assets/38593134/8072a566-5bf0-4f05-9994-808145406bdc">
        <img alt="Defender Remover" src="https://user-images.githubusercontent.com/79479952/239704528-c017473e-1d2a-4d4a-a215-bf71d137b86a.png">
    </picture>
</a>

## ❓️ What does the app do?

This application removes / disables Windows Defender, including the Windows Security App, Windows Virtualization-Based Security (VBS), Windows SmartScreen, Windows Security Services, Windows Web-Threat Service, Windows File Virtualization (UAC), Microsoft Defender App Guard, Microsoft Driver Block List, System Mitigations and the Windows Defender page in the Settings App on Windows 10 or later.

## 🖍 System Requirements

* Windows `8.x`, `10` and `11` (all versions).


## 📃 Instructions

> [!NOTE]
> A system restore point is recommended before you run the script.

1. Download the packed script from [Releases](https://github.com/jbara2002/windows-defender-remover/releases)
2. Run the ".exe" as administrator
3. Follow the instructions displayed

![cli](https://github.com/drunkwinter/windows-defender-remover/assets/38593134/46007191-0a65-43c2-b451-a993ff90e00e)

Please file an [issue](https://github.com/ionuttbara/windows-defender-remover/issues) if you experience any problems.

## 📃 Automation of the script

You can disable or enable Windows Defender with arguments.

#### Enable/Disable Windows Defender and Security Components

```PowerShell
# ENABLE
Defender.Remover.exe /r <# or /R #>

# DISABLE
Defender.Remover.exe /n <# or /N #>
```

#### Enable/Disable Windows Defender Antivirus only

```PowerShell
# ENABLE
Defender.Remover.exe /e <# or /E #>

# DISABLE
Defender.Remover.exe /m <# or /M #>
```

## Disable or Remove Windows Defender *Application Guard Policies* (advanced)

If you have any problems when opening an app (*extremely rare*) and get the message "The app can not run because Device Guard" or "Windows Defender Application Guard Blocked this app", you have to remove 4 files with the same name, from different locations.


- In EFI Partition

```PowerShell
Remove-Item -LiteralPath "$((Get-Partition | ? IsSystem).AccessPaths[0])Microsoft\Boot\WiSiPolicy.p7b"
```

- In Code Integrity Folder

```PowerShell
Remove-Item -LiteralPath "$env:windir\System32\CodeIntegrity\WiSiPolicy.p7b"
```

- In Windows Folder

```PowerShell
Remove-Item -LiteralPath "$env:windir\Boot\EFI\wisipolicy.p7b"
```

- In WinSxS Folder

```PowerShell
Remove-Item -Path "$env:windir\WinSxS" -Include *winsipolicy.p7b* -Recurse
```

## ❓ Frequently Asked Questions

#### ⭕ Why is the downloaded executable being flagged as a virus?

That is a false positive.

Some security apps flag this app as a virus because of the way the ".exe" files are created.

#### ⭕ Why is the patch not working when Windows is updated?

Windows Update includes a ```Intelligence Update``` which blocks certain actions and modifies Windows Defender/Security policies.
If the script is not working for you, check if you have the Windows Security Intelligence Update installed. If you do, disable tamper protection, and re-run the script.

#### ⭕ How to use the package remover without downloading the executable from the release?

Run the desired ".bat" file from cmd with PowerRun (by dragging to the executable). You must reboot for the changes to take effect.
