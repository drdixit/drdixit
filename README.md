# <b>(•ᴥ•)ゞ&nbsp;&nbsp;&nbsp;Salutations!<br>&nbsp;&#8201;/|\\<br>&nbsp;&#8201;/ \\</b><br>![](https://visitor-badge.laobi.icu/badge?page_id=drdixit.drdixit)
# <br>⚠️ Warning: "use your credentials, paths and everything"
# Windows 11 Cheat Sheet
## powershell config
Location ~ `C:\Users\user\Documents\PowerShell\Microsoft.PowerShell_profile.ps1` If not already exist create it<br>
Ex `whereis git` and it returns path of node `C:\Users\user\scoop\shims\git.exe`<br>
Useful for checking like if you have two exes are installed on the system like which one is currently in use.
```powershell
function whereis ($command) {
	Get-Command -Name $command -ErrorAction SilentlyContinue |
	Select-Object -ExpandProperty Path -ErrorAction SilentlyContinue
}
```
change the default prompt
```powershell
function prompt {
    $esc = [char]27
    $reset = "$esc[0m"
    $cyan = "$esc[36m"
    $green = "$esc[32m"
    $red = "$esc[31m"
    $yellow = "$esc[33m"

    $currentPath = Get-Location
    $gitBranch = ''
    $gitStatus = ''

    if (Test-Path .git) {
        $gitBranch = git rev-parse --abbrev-ref HEAD 2>$null
        $statusOutput = git status --porcelain 2>$null
        if ($statusOutput) {
            $gitStatus = '*'
        }
    }

    "$cyan$currentPath $green$gitBranch$gitStatus$yellow✘$reset "
}
```


[go here install scoop and git](https://scoop.sh/)<br>
quick tip i installed git with winget --scope machine and its giving me problems i have to use sudo + inline to work and sometimes it didn't even work.<br>
feture self please use scoop for git<br>
admin and scope user both have different execuation policies setup wisely.<br>
this thig is also useful for nodejs like script execution disabled or something.<br>
Current execution policy check
```powershell
Get-ExecutionPolicy
```
Set Execution Policy
```powershell
Set-ExecutionPolicy unrestricted
```
# Git section
generate the keys
```powershell
ssh-keygen -t ed25519 -C "drdixit6@gmail.com"
```
set username globally
```powershell
git config --global user.name "Dixit"
```
set email globally
```powershell
git config --global user.email "drdixit6@gmail.com"
```
Tells Git to use SSH keys (not GPG) for commit signing.
```powershell
git config --global gpg.format ssh
```
Sets the public SSH key file you want Git to use for signing commits. Replace the path if your key is elsewhere.<br>
```powershell
git config --global user.signingkey C:\Users\user\.ssh\id_ed25519.pub
```
Makes Git sign all commits by default, so you don’t have to add -S every time.
```powershell
git config --global commit.gpgsign true
```
**Not Mandatory** but you can do this<br>
Some Windows Things (Run Powershell as Admin)<br>
This ensures the ssh-agent starts every time you log into Windows
```powershell
Get-Service ssh-agent | Set-Service -StartupType Automatic
```
Currently start ssh agent service
```powershell
Start-Service ssh-agent
```
Add your keys to ssh-agent (after pasting try hitting with tab does it autocomplete to absolute path)
```powershell
ssh-add %USERPROFILE%\.ssh\id_ed25519
```
Verify the key is loaded
```powershell
ssh-add -l
```



# ASCI Section
| Char Code | Size | Width |
|-----------|------|-------|
|`&nbsp;`|─&nbsp;─||
|`&#8201;`|─&#8201;─|~1/5 space|
|`&#8202;`|─&#8202;─|Very thin|
|`&#8239;`|─&#8239;─|Slightly thinner than `&nbsp;`|


last git config
```powershell
C:\motobill [stock ≡]> cat C:\Users\mail\.gitconfig
[user]
        name = Dixit
        email = drdixit6@gmail.com
        signingkey = C:\\Users\\mail\\.ssh\\id_ed25519.pub
[gpg]
        format = ssh
[commit]
        gpgsign = true
[gpg "ssh"]
        program = C:/Windows/System32/OpenSSH/ssh-keygen.exe
```

i also added this to my git config
```powershell
PS C:\Users\mail> cat .\.gitconfig
[user]
        name = Dixit
        email = drdixit6@gmail.com
        signingkey = C:\\Users\\mail\\.ssh\\id_ed25519.pub
[gpg]
        format = ssh
[commit]
        gpgsign = true
[gpg "ssh"]
        program = C:/Windows/System32/OpenSSH/ssh-keygen.exe
        allowedSignersFile = C:/Users/mail/.config/git/allowed_signers
```

I also added this as well
```powershell
PS C:\motobill> git config --global push.autoSetupRemote true
```
```powershell
PS C:\motobill> cat C:\Users\mail\.gitconfig
[user]
        name = Dixit
        email = drdixit6@gmail.com
        signingkey = C:\\Users\\mail\\.ssh\\id_ed25519.pub
[gpg]
        format = ssh
[commit]
        gpgsign = true
[gpg "ssh"]
        program = C:/Windows/System32/OpenSSH/ssh-keygen.exe
        allowedSignersFile = C:/Users/mail/.config/git/allowed_signers
[push]
        autoSetupRemote = true
```

log for my reference
cmd as admin
```cmd
setx HOME "%USERPROFILE%" /M
setx XDG_CONFIG_HOME "%USERPROFILE%\.config" /M
setx XDG_DATA_HOME "%USERPROFILE%\.local\share" /M
setx XDG_STATE_HOME "%USERPROFILE%\.local\state" /M
setx XDG_CACHE_HOME "%USERPROFILE%\.cache" /M
```
