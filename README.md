# <b>(•ᴥ•)ゞ&nbsp;&nbsp;&nbsp;Salutations!<br>&nbsp;&#8201;/|\\<br>&nbsp;&#8201;/ \\</b>
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


log for my reference
cmd as admin
```cmd
setx HOME "%USERPROFILE%" /M
setx XDG_CONFIG_HOME "%USERPROFILE%\.config" /M
setx XDG_DATA_HOME "%USERPROFILE%\.local\share" /M
setx XDG_STATE_HOME "%USERPROFILE%\.local\state" /M
setx XDG_CACHE_HOME "%USERPROFILE%\.cache" /M
```

powershell as admin
```powershell
winget install --scope machine --source winget Microsoft.VisualStudio.2022.BuildTools --force --override "--passive --wait --add Microsoft.VisualStudio.Workload.VCTools --includeRecommended --includeOptional"
```
normal terminal powershell
```powershell
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression

scoop install main/git
reg import "C:\Users\mail\scoop\apps\git\current\install-file-associations.reg"

scoop bucket add extras
scoop install extras/posh-git
Add-PoshGitToProfile
```
git setup normal terminal
```powershell
C:\Users\mail> ssh-keygen -t ed25519 -C "drdixit6@gmail.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\mail/.ssh/id_ed25519):
Created directory 'C:\\Users\\mail/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\mail/.ssh/id_ed25519
Your public key has been saved in C:\Users\mail/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:rWudscCF9jXSbwXxHSYI/SuzD.... drdixit6@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|         .o ...+ |
....
|       o*..      |
+----[SHA256]-----+
C:\Users\mail> cat .\.ssh\id_ed25519.pub
ssh-ed25519 AAAAC3NzaC1lZDI1N.... drdixit6@gmail.com
C:\Users\mail> git config --global user.name "Dixit"
C:\Users\mail> git config --global user.email "drdixit6@gmail.com"
C:\Users\mail> git config --global gpg.format ssh
C:\Users\mail> git config --global user.signingkey C:\Users\user\.ssh\id_ed25519.pub
C:\Users\mail> git config --global commit.gpgsign true
C:\Users\mail> 
C:\Users\mail> git config --global gpg.ssh.program "C:/Windows/System32/OpenSSH/ssh.exe"
```
```powershell
powershell as admin
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Install the latest PowerShell for new features and improvements! https://aka.ms/PSWindows

Loading personal and system profiles took 838ms.
C:\WINDOWS\system32> Get-Service ssh-agent | Set-Service -StartupType Automatic
C:\WINDOWS\system32> Start-Service ssh-agent
C:\WINDOWS\system32> Add your private key (note: use PRIVATE key, not .pub)^C
C:\WINDOWS\system32> ssh-add $env:USERPROFILE\.ssh\id_ed25519
Identity added: C:\Users\mail\.ssh\id_ed25519 (drdixit6@gmail.com)
C:\WINDOWS\system32> ssh-add -l
256 SHA256:rWudscCF9jXSbw... drdixit6@gmail.com (ED25519)
C:\WINDOWS\system32>
```
normal terminal
```powershell
C:\Users\mail> git config --global user.signingkey ~/.ssh/id_ed25519.pub
C:\Users\mail> cat .\.gitconfig
[user]
        name = Dixit
        email = drdixit6@gmail.com
        signingkey = ~/.ssh/id_ed25519.pub
[gpg]
        format = ssh
[commit]
        gpgsign = true
[gpg "ssh"]
        program = C:/Windows/System32/OpenSSH/ssh.exe
C:\Users\mail> git config --global user.signingkey C:\Users\mail\.ssh\id_ed25519.pub
C:\Users\mail> cat .\.gitconfig
[user]
        name = Dixit
        email = drdixit6@gmail.com
        signingkey = C:\\Users\\mail\\.ssh\\id_ed25519.pub
[gpg]
        format = ssh
[commit]
        gpgsign = true
[gpg "ssh"]
        program = C:/Windows/System32/OpenSSH/ssh.exe
```
i still have my doubts about / \\ or ~/ in path but final one works with signing key with \\ and program with /

oh shit i made a mistake

for ssh signing you need to use ssh-keygen not ssh
## i will refactore this in future

also, your signing key should point to the private key, not the public key i am so stupid

```powershell
C:\motobill [stock ≡ +0 ~1 -0 ~]> cat C:\Users\mail\.gitconfig
[user]
        name = Dixit
        email = drdixit6@gmail.com
        signingkey = C:\\Users\\mail\\.ssh\\id_ed25519.pub
[gpg]
        format = ssh
[commit]
        gpgsign = true
[gpg "ssh"]
        program = C:/Windows/System32/OpenSSH/ssh.exe
C:\motobill [stock ≡ +0 ~1 -0 ~]> git config --global user.signingkey "C:\Users\mail\.ssh\id_ed25519"
C:\motobill [stock ≡ +0 ~1 -0 ~]> git commit -m "test"
error: ssh: Could not resolve hostname sign: No such host is known. ?

fatal: failed to write commit object
C:\motobill [stock ≡ +0 ~1 -0 ~]> git config --global gpg.ssh.program "C:/Windows/System32/OpenSSH/ssh-keygen.exe"
C:\motobill [stock ≡ +0 ~1 -0 ~]> git commit -m "test"
[stock 092a51b] test
 1 file changed, 1 deletion(-)
C:\motobill [stock ↑1]> git push
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 12 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 633 bytes | 633.00 KiB/s, done.
Total 5 (delta 4), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (4/4), completed with 4 local objects.
To github.com:drdixit/motobill.git
   7f16c23..092a51b  stock -> stock
C:\motobill [stock ≡]> cat C:\Users\mail\.gitconfig
[user]
        name = Dixit
        email = drdixit6@gmail.com
        signingkey = C:\\Users\\mail\\.ssh\\id_ed25519
[gpg]
        format = ssh
[commit]
        gpgsign = true
[gpg "ssh"]
        program = C:/Windows/System32/OpenSSH/ssh-keygen.exe
```


