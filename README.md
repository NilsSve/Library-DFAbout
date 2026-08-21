# DFAbout

A drop-in replacement for the DataFlex **About** dialog, for Windows desktop applications.

Instead of a static box you maintain by hand, DFAbout fills itself in: the application name and
version come from the program's own settings, the build date comes from the compiled `.exe`, and a
second panel reports the machine the program is actually running on — which is usually the first
thing you need when a user reports a problem.

## What the dialog shows

- **Application name, version, copyright and author** — name and version are read from the
  application's own settings when you leave them blank
- **Compile date and time**, taken from the executable itself, so it is always the build in front
  of you rather than a constant somebody forgot to update
- **A system information panel** — computer name, network user, installed and available memory,
  and the SQL client version when one is in use
- **Code-signing details** for the running executable, when a signed build is in use
- **A copy button**, so a user can paste the whole report into an email or a support ticket
- Your own logo, or the supplied *Powered by DataFlex* image

## Installing

**DataFlex 26 and later** — add it as a package:

```
https://github.com/NilsSve/Library-DFAbout.git/DFAbout26.0.sws
```

**DataFlex 25** — add `DFAbout25.0.sws` as a library in your workspace.

## Using it

Use the package and override `Activate_About` in your application:

```dataflex
Use StdAbout.pkg

Procedure Activate_About
    Send DoAbout "My Application" "" "Copyright 2026, My Company" "Written by A. Developer" "MyLogo.bmp"
End_Procedure
```

Every argument is optional. Leave the title or version blank and DFAbout takes them from the
application settings; leave the bitmap blank and it uses the supplied DataFlex image:

```dataflex
Procedure Activate_About
    Send DoAbout "" "" ("Copyright 2026" * psCompany(ghoApplication)) "" ""
End_Procedure
```

`DoAbout` accepts up to ten arguments; the later ones add extra lines such as an internet address
or a support contact.

### Compile date on its own

The build timestamp is also available without the dialog:

```dataflex
DateTime dtBuilt
Move (ProgramCompileDate(psProgramName(ghoApplication))) to dtBuilt
```

### Code-signing details

To show certificate information for the running program, place Microsoft's `signtool.exe` in the
application's `Programs` folder. Without it the rest of the dialog works normally and the
signing section is simply absent.

## Requirements

DataFlex 25 or 26, Windows desktop. DFAbout has no dependencies on other libraries.

## Licence

MIT — see [LICENSE](LICENSE).
