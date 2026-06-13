# BitLocker und Windows-Vorbereitung

## Warum das wichtig ist

BitLocker verschluesselt Windows-Laufwerke. Aenderungen an Bootloader, Partitionen oder UEFI koennen dazu fuehren, dass Windows beim naechsten Start den BitLocker-Wiederherstellungsschluessel verlangt.

Ohne diesen Schluessel kann der Zugriff auf Windows blockiert sein.

## BitLocker pruefen

Eingabeaufforderung als Administrator:

```cmd
manage-bde -status C:
manage-bde -protectors -get C:
```

PowerShell als Administrator:

```powershell
Get-BitLockerVolume -MountPoint "C:"
(Get-BitLockerVolume -MountPoint "C:").KeyProtector
```

## GUI-Weg

1. Systemsteuerung oeffnen
2. BitLocker-Laufwerkverschluesselung suchen
3. Laufwerk `C:` pruefen
4. Wiederherstellungsschluessel sichern
5. Schluessel nicht nur auf Laufwerk `C:` speichern

## BitLocker voruebergehend aussetzen

Erst ausfuehren, wenn der Recovery-Key wirklich gesichert ist.

Eingabeaufforderung als Administrator:

```cmd
manage-bde -protectors -disable C: -RebootCount 2
```

PowerShell als Administrator:

```powershell
Suspend-BitLocker -MountPoint "C:" -RebootCount 2
```

## Wichtig

Dual Boot nur, wenn der BitLocker-Recovery-Key vorliegt. Ohne Key wird VirtualBox genutzt oder auf einem ungenutzten Geraet installiert.
