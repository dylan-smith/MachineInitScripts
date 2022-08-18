# PowerShell Scripts

These scripts are my custom profile scripts for PS command windows and for ISE including
a custom "Dark Selenitic" theme for ISE.

## How to install

This entire repo can be overlayed ontop of your Documents\WindowsPowerShell folder.

As with all PowerShell scripts, you'll need to loosen up the execution policy on new machines.

```powershell
Set-ExecutionPolicy RemoteSigned -Force -Confirm:$false;
Set-Executionpolicy -Scope CurrentUser -ExecutionPolicy UnRestricted -Force -Confirm:$false
```

Future: _I'll consider signing the scripts and setting the execution policy to AllSigned._

#### Installation options:

This is the best option for keeping up to date using the update-profile command:

```powershell
Set-Location $env:USERPROFILE\Documents;
git clone https://github.com/stevencohn/WindowsPowerShell.git
```

Or to download the repo as a Zip file then you'll need to unblock all files:

```powershell
Get-ChildItem -Path "${env:USERPROFILE}\Documents\WindowsPowerShell" -Recurse | Unblock-File
```

Or to download just the [Initialize-Machine.ps1](#setup) script:

```powershell
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]'Ssl3,Tls,Tls11,Tls12';
Invoke-WebRequest -Uri 'https://raw.githubusercontent.com/stevencohn/WindowsPowerShell/main/Initialize-Machine.ps1' -OutFile C:\Initialize-Machine.ps1
```

See also the [Install-Programs.ps1](#setup) script below.

## Commands
These scripts are located in the Modules\Scripts folder.

#### [`Clear-Events`](Modules/Scripts/Clear-Events.ps1) [-Quiet]
Clear all events from the Windows Event Log.

#### `Clear-Temp` [-Quiet]
Clear the contents of TEMP, Windows\TEMP, and LocalAppData\TEMP.

#### `ConvertFrom-BinHex` -Hex v -Unicode
Convert a BinHex encoded string back to its original string value.

#### `ConvertFrom-Hex` -Hex v
Convert a Hex string into an integer value. If the string contains six
or eight characters then it is also interpreted as an ARGB value and each
component part is displayed.

#### `ConvertTo-Hex` -R r [-G g] [-B b]
Convert integer values to a Hex string. If one integer is specified then it is converted. If three integers are specified then they are assumed to be RGB values and combined into a single Hex string.

#### `ConvertTo-mp3` -InputPath p [-Bitrate r] [-FullQuality] [-Info] [-Yes]
Primarily used to convert .m4a audio files to .mp3

#### `Copy-Console` [-OutFile f] [-All] [-Rtf] [-Trim]
Copy the contents of the Powershell console window preserving color. Can be sent to an out file or pasted into Word or OneNote.

#### `Copy-Playlist` -Playlist p -Target t -WhatIf
Copies all music files referenced by the given playlist to the specified location.
For example, this can be used to copy music in an .m3u playlist file to a USB thumbdrive.

#### `Edit-Hosts`
Open the hosts file in Notepad.

#### `Enable-MultiRdp` [-MaxConnection m]
Patch termsrv.dll to allow multiple concurrent RDP connections to this machine

#### `Edit-Playlist` -Replace r [-Path p] [-Type t]
Replace the path of all items in a playlist file to the current user's MyMusic path.

#### `Edit-PSProfile`
Run VSCode with ~Documents\WindowsPowerShell as root folder. Aliased to `ep`

#### `Enable-PersonalOneDrive`
Enable Personal OneDrive sync when both Business and Personal accounts are registered
on the local machine. Will indicate when either is account not available.

#### `Enable-TrustedRemoting`
Enable PowerShell remoting and trusted hosts for the current machine,
typically run on a VM that will be used for automated tasks such as CI/CD.

#### `Get-Account` -Username u [-Domain d] [-SID]
Report the account information for the given username and optionally a specified domain.

![alt text](Images/get-account.png "Get-Account Example")

#### `Get-ChildItemColorized` -Dir d [-la]
Display a colorized directory listing along with total size. Aliased to `ls`

![alt text](Images/get-childitemcolorized.png "Get-ChildItemColorized Example")

#### `Get-Colors` [-All] [-Cmd] [-PS] [-ConEmu] [-Script]
Display the console colors for Command console, PowerShell console, and ConEmu consoles.

![alt text](Images/get-colors.png "Get-Colors Example")

#### `Get-CommandLine` [-Name n] [-Only] [-ReturnValue] [-ShowSystem]
Report processes with their command lines, highlighting an optional search string

#### `Get-Commits` -Project p [-Branch b] [-Since yyyy-mm-dd] [-Last n] [-Raw] [-Graph]
Reports all commits for the given git repo after a specified date or within the last n days.

#### `Get-DirSize` -Dir d [-la]
Report the size of all items in the specified folder. Used as a sub-routine of Get-ChildItemColorized.

#### `Get-DotNetVersion`
Get the versions of.NET Framework installations on the local computer.

#### `Get-Env` [-Name n] [-Value v]
Report environment variables in colorized categoties with optional search highlighting.

![alt text](Images/get-env.png "Get-Env Example")

#### `Get-Hosts`
Display the /etc/hosts file, colorized.

#### `Get-Installed` [-Outfile f]
Report all installed applications registered on the local system.

#### `Get-Network` [-Preferred] [-Addresses] [-Verbose]
Determines the most likely candidate for the active Internet-specific network adapter on this machine.  All other adpaters such as tunneling and loopbacks are ignored.  Only connected IP adapters are considered. Wifi aliases are shown.

![alt text](Images/get-network.png "Get-Network Example")

#### `Get-ParentBranch`
Determine the name of the nearest parent branch of the current branch in the local Git repo.

#### `Get-Path` [-Search s] [-Sort] [-Verbose]
Display the PATH environment variable as a list of strings rather than a single string and displays the source of each value defined in the Registry: Machine, User, or Process. Verbose mode dumps the User and System Paths as
stored in the Windows Registry.

![alt text](Images/get-path.png "Get-Path Example")

#### `Get-Performance`
Get and report performance metrics using the built-in WinSAT utility.

#### `Get-Scripts`
List all external scripts and their parameter names.

#### `Get-Services` [-Name n] [-Running || -Stopped]
Get a list of services ordered by status and name. Aliased to `gs`

#### `Get-SpecialFolder` [-Folder f] [-All]
Return the translation of a SpecialFolder by name or show all SpecialFolders with optional search highlighting.

#### `Get-VMConfig` -Path p [-Json]
Returns a VM configuration object of the specified .vmcx VM configuration
file even if the VM is not attached to a Hyper-V server.

#### `Install-BuildTools` [-Force] [-Full] [-VsWhere]
Install minimal Microsoft build and test tools required for CI/CD.

#### `Install-Chocolatey` [-Upgrade]
Can be used on new machines to install Chocolately. If already installed then checks if it is outdated and prompts to update.

#### `Install-Docker`
Installs Docker for Windows, enabling Hyper-V as a prerequisite if not already installed.

#### `Invoke-NormalUser` -Command c
Execute a given command as a non-evelated context. Aliased to `nu`. 
Convenient when you need to run as a normal user from an elevated prompt.

#### `Invoke-SuperUser`
Open a new command prompt in elevated mode. Aliased to `su`. Special command for ConEmu emulator.

#### `Invoke-VsDevCmd`
Invoke the Visual Studio environment batch script. Aliased to `vs`

#### `New-Administrator` -Username -Password
Create a new local admin user.

#### `New-CommandWrapper`
Sepcial internal function from PowerShell Cookbook.

#### `New-DriveMapping` -DriveLetter d -Path p [-SourceDriveLabel s] [-DriveLabel l] [-Reboot] [-Force]
Create a persistent mapping of a folder to a new drive letter. (persistent SUBST)

#### `New-Host` -IP a -Name n
Adds or updates an entry in the Windows hosts file

#### `New-RunAsShortcut` -LinkPath l -TargetPath t [-Arguments a]
Creates a new elevated shortcut (.lnk file) to a given target

#### `New-VMClone` -Name n -Path p -Template t [-Checkpoint]
Create a new VM from a registered VM or an exported VM.

#### `PrettyPrint-File` -Path p [-Dedent] [-Overwrite]
Format or pretty-pretty JSON and XML files.

#### `Remove-DockerTrash` [-Volumes]
Prune unused docker containers and dangling images.

#### `Remove-DriveMapping` -DriveLetter d [-SourceDriveLabel s] [-Reboot] [-Force]
Remove a persistent mapping of a folder created by New-DriveMapping.

#### `Remove-Locked` -Name n
Remove a System-owned file or directory. Attempts multiple approaches to remove stubborn items.

#### `Repair-Path` [-Yes]
Clean up the PATH environment variable, removing duplicates, empty values, invalid paths, repairs
variable substitutions, and moves paths between User and System paths appropriately.
Verbose mode dumps the User and System Paths as stored in the Windows Registry.

#### `Restart-App` -Name [-Command [-Arguments]] [-Register] [-GetCommand]
Restart the named process. This can be used to restart applications such as Outlook on a nightly
basis. Apps such as this tend to have memory leaks or become unstable over time when dealing with
huge amounts of data on a very active system. The -Register switch creates a nightly automation task.

#### `Restart-Bluetooth` [-Show]
Restarts the Bluetooth radio device on the current machine. This is useful when the radio stops
communicating with a device such as a mouse. The alternative would be to reboot the system.

#### `Set-Colors` -Theme t | [-Name n -Color c [-Bgr] [-Background] [-Foreground]] [-Cmd] [-ConEmu] [-PS]
Set the color theme for command line consoles or set a specific named color.

#### `Set-ItemOwner` -Path p [-Group g]
Set the ownership of an item - folder or file - to the specified user group.

#### `Set-OutDefaultOverride`
(Internal) Helper function for Get-ChildItemColorized.

#### `Set-PinTaskbar` -Target t [-Unpin]
Pins or unpins a target item to the Windows Taskbar (_currently broken!_)

#### `Set-RegistryOwner` -Hive h -Key k [-Recurse]
Set full-access ownership of a specified Registry key.

#### `Set-SleepSchedule` (-SleepTime -WakeTime) | (-Clear [-ClearTimers])
Creates scheduled tasks to sleep and wake the computer at specified times.

#### `Show-ColorizedContent` -Filename f [-ExcludeLineNumbers]
Type the contents of a PowerShell script with syntax highlighting.

![alt text](Images/show-colorizedcontent.png "Show-ColorizedContent Example")

#### `Show-Docker` [-Ps] [-Containers] [-Images] [-Volumes]
Show containers and images in a single command.

![alt text](Images/show-docker.png "Show-Docker Example")

#### `Start-VMUntilReady` -Name n [-Restart] [-Restore]
Start the named VM, optionally restoring the latest snapshot, and waiting
until the OS provides a stable heartbeat.

#### `Test-Elevated` [-Action a ] [-Warn]
Determine if the current session is elevated and displays a warning message if not.
Can be run without the warning message and simply return a boolean result.

#### `Test-RebootPending` [-Report]
Check the pending reboot status of the local computer.

#### `Update-Environment`
Refresh the current session environment variables from the Registry by harvesting
from both the local machine and the current user hives.

#### `Update-Gits` [-Branch b] [-Project p] [-Reset]
Scan all sub-folders looking for .git directories and fetch/pull each to get latest code.

#### `Update-Profile`
Quick command line to pull latest source of this WindowsPowerShell repo from Github
and update the content in $home\Documents\WindowsPowerShell.

<a name="setup"></a>

# Setup

#### [`Initialize-Machine.ps1`](Initialize-Machine.ps1) [-Command c] [-ListCommands] [-RemoveOneDrive] [-RemoveCortana]
This is a top-level script meant to be downloaded independently from this repo and run to configure and
initialize new machines. This script will download this repo to the current user's Document folder,
setting it up as the default PowerShell profile. Best to download it to and run from the root of C.

Run `Set-ExecutionPolicy RemoteSigned` prior to running if this is the first use of PowerShell.

The Initialize-Machine script will download this repo into the MyDocuments folder, but
if you have OneDrive enabled then the MyDocuments folder may differ from $home\Documents.
So before initializing, you can create a junction point to MyDocuments using this command:

   1. `cd $home\Documents` 
   1. `cmd 'mklink /j WindowsPowerShell ([Environment]::GetFolderPath('MyDocuments'))`

Since this updates the PowerShell console colors, you can close and reopen the console to
appreciate these fantastic new colors.

#### [`Install-HyperV.ps1`](Install-HyperV.ps1)
Automates the installation of Hyper-V on Windows 11 for either Professional or
Home editions. The script doesn't require any parameters but will prompt to reboot
the computer to complete the configuration.

#### [`Install-Programs.ps1`](Install-Programs.ps1)
Automates the installation of applications, development tools, and other utilities.
All applications, including Visual Studio, install unattended in about 25 minutes.
It's also reentrant, skipping items already installed and installing items missing.

`.\Install-Programs.ps1 [-Command c] [-ListCommands] [-Extras] [-Verbose]`
 
   * _command_ - optional argument to run a single command, default is to run all commands
   * -AccessKey - optional, store your AWS access key in your private awscli config
   * -SecretKey - optional, store your AWS secret key in your private awscli config
   * -ListCommands - this argument displays all available commands
   * -Extras - this argument causes extra applications to be installed
   * -Vebose - print extra information for each command

Hyper-V is required for a couple of command and warning will be displayed if it is not yet
available. Use Install-HyperV to enable Hyper-V prior to running Install-Programs.

Default applications:

   * 7Zip
   * Angular (_specific version_)
   * AWSCli
   * BareTail Free (_installed to C:\tools_)
   * Curl
   * Docker Desktop
   * Git
   * Greenfish Icon Editor Pro
   * Greenshot
   * LINQPad
   * Macrium Reflect Free (_installer_)
   * mRemoteNG
   * Node.js (_specific version_)
   * Notepad++
   * Nuget command line
   * Robot3T
   * S3Browser
   * SharpKeys
   * SysInternals procexp and procmon
   * Windows Terminal

Other applications included when -Extras is specified

   * Audacity audio editor
   * DateInTray (_installed to C:\tools_; Win10 only)
   * Dopamine music player
   * Paint.net
   * TreeSize Free
   * VLC
   * WiLMa (_installed to C:\tools_)

During the installation, hints and tips are shown highlighted in yellow and
instructions are highlighted in cyan. Some are import, such as how to continue
the manual installation of Macrium.

### Reminders shown after a full install

Macrium Reflect

   1. Double-click the Macrium Installer icon on the desktop after VS is installed
   1. Choose Free on first screen, then Home version, and no registration is necessary

Consider these manually installed apps:
- AVG Antivirus
- BeyondCompare (there is a choco package but not for 4.0)
- ConEmu
- OneMore OneNote add-in (https://github.com/stevencohn/OneMore/releases)

# [`Install-VS.ps1`](Install-VS.ps1)
Standalone script to install Visual Studio and its extensions or VSCode and its extensions.
The default is to install VS Professional.

`.\Install-VS.ps1 [-Community|Professional|Enterprise|Extensions] [-Verbose]`

   * Visual Studio 2019 _and extensions_ (_professional or enterpise_)
   * VSCode _and extensions_

When installing VS, let it complete and then rerun this script with the -Extensions parameter
to install common extensions.

# Profiles

### Microsoft.PowerShell_profile.ps1

This the primary PowerShell profile definition script, run whenenver a new PowerShell command
prompt is open or session is created. It defines aliases for some of the commands above. It also
invokes special utilities unique to my environment such as integration with ConEmu, WiLMa, 
Chocolatey, and setting the intial working directory.

#### Console Prompt Customization

The PowerShell command prompt is customized as follows:

   * It is rendered in blue
   * It indicates the current working directory prefaced with "PS" for example `PS D:\code>`
   * If the console is elevated then the "PS" prefix is shown in red to highlight the fact that what do you, you do at your own risk!

  ![alt text](Images/ps-prompt.png "Colorized PS Prompt Example")


### Microsoft.PowerShellISE_profile.ps1

This is the profile definition script fort the PowerShell ISE editor. It registers ISE add-ons
found in the Modules\Addons folder.

### Microsoft.VSCode_profile.ps1

This is the profile definition script for the VSCode integrated PowerShell terminal.
It simply invokes the primary profile script above.

# Dark Selenitic Scheme

The `Dark Selenitic.StorableColorTheme.ps1xml` file defines the Dark Selenitic color scheme for ISE. The theme is also
defined by the Themes\PSTheme_Selenitic.ps1 script.
