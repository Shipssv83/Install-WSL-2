Hi, ![](https://user-images.githubusercontent.com/18350557/176309783-0785949b-9127-417c-8b55-ab5a4333674e.gif)my name is Serhii Shypylov
=========================================================================================================================================

-------------------------------

### Socials
<p align="left">
  <a href="https://t.me/oneitpro">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/telegram-app.png" alt="Telegram" width="30" height="30" />
  </a>
  <a href="https://www.linkedin.com/in/sergey-shipilov-7262a31b4/">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/linkedin.png" alt="LinkedIn" width="30" height="30" />
  </a>
  <a href="https://www.instagram.com/shipssvpl/">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/instagram-new.png" alt="Instagram" width="30" height="30" />
  </a>
  <a href="https://www.facebook.com/profile.php?id=100083345006373">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/facebook.png" alt="Facebook" width="30" height="30" />
  </a>
  <a href="https://discord.com/invite/6z5EyagDyW?ref=1it.pro">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/discord.png" alt="Discord" width="30" height="30" />
  </a>
  <a href="mailto:admin@1it.pro">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/new-post.png" alt="Mail" width="30" height="30" />
  </a>
  <a href="https://1it.pro/">
    <img src="https://img.icons8.com/ios-glyphs/30/ffffff/domain.png" alt="Website" width="30" height="30" />
  </a>
</p>

# Install-WSL-2
PowerShell скрипт, который автоматизирует процесс включения функций для WSL, установки WSL 2 и дистрибутива Linux в Windows:
```powershell
# PowerShell скрипт для настройки и установки WSL и дистрибутива Linux на Windows

# Включение компонентов WSL и платформы виртуальной машины
Write-Output "Включение компонентов Windows для WSL и виртуальной машины..."
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux -All -NoRestart
Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform -All -NoRestart

# Перезагрузка компьютера, если требуется
if ($LASTEXITCODE -eq 3010)
{
    Write-Output "Требуется перезагрузка для завершения установки компонентов."
    Read-Host "Нажмите Enter для перезагрузки..."
    Restart-Computer
}

# Скачивание и установка пакета обновления ядра Linux для WSL 2
$kernelUpdateUrl = "https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi"
$kernelUpdatePath = "$env:USERPROFILE\Downloads\wsl_update_x64.msi"

Write-Output "Скачивание пакета обновления ядра Linux для WSL 2..."
Invoke-WebRequest -Uri $kernelUpdateUrl -OutFile $kernelUpdatePath

Write-Output "Установка пакета обновления ядра Linux..."
Start-Process msiexec.exe -ArgumentList "/i", $kernelUpdatePath, "/quiet", "/norestart" -Wait

# Установка WSL 2 как версии по умолчанию
wsl --set-default-version 2

# Установка дистрибутива Linux (Ubuntu) из Microsoft Store
# Убедитесь, что у вас настроен Microsoft Store для скриптов или установите дистрибутив вручную
Write-Output "Установка дистрибутива Ubuntu..."
winget install -e --id Canonical.Ubuntu

Write-Output "Настройка завершена. Теперь вы можете использовать Ubuntu на вашем компьютере с Windows."
```
