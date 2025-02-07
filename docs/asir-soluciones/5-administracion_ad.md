# EJERCICIOS DE ADMINISTRACIÓN DE ACTIVE DIRECTORY (AD DS)  

## 1. Creación automatizada de usuarios en AD DS a partir de un archivo CSV  
Se ha decidido crear el **AD DS de la FIFA-2018**, donde:  
- Cada usuario representa un **jugador**.  
- Cada **club** será un grupo en Active Directory.  
- Se utilizará **PowerShell** para importar los usuarios desde un archivo CSV y asignarlos a sus respectivos grupos.  

 
```powershell
Import-Module ActiveDirectory

# Ruta del archivo CSV
$csvPath = "C:\ruta\a\jugadores.csv"
$jugadores = Import-Csv -Path $csvPath

foreach ($jugador in $jugadores) {
    # Definir el nombre de usuario
    $username = $jugador.Username
    
    # Crear el usuario en AD
    New-ADUser -Name "$($jugador.FirstName) $($jugador.LastName)" `
        -GivenName $jugador.FirstName `
        -Surname $jugador.LastName `
        -SamAccountName $username `
        -UserPrincipalName "$username@FIFA18.com" `
        -Path "OU=Jugadores,DC=FIFA18,DC=com" `
        -AccountPassword (ConvertTo-SecureString $jugador.Password -AsPlainText -Force) `
        -Enabled $true

    # Asignar el usuario al grupo del club
    $grupo = $jugador.Club
    if (Get-ADGroup -Filter {Name -eq $grupo}) {
        Add-ADGroupMember -Identity $grupo -Members $username
    } else {
        Write-Host "El grupo '$grupo' no existe."
    }
}
```
