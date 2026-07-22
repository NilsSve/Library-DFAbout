# DFAbout
 Extended DFAbout dialog. This is a library used by main repositories on this site (not libraries)! It is being installed automatically when cloning one of the main repositories.

## Dependencies

None. DFAbout is a leaf: no `[Libraries]` in its `.sws`, no submodules, and nothing in its
packages reaches into another RDC library. Please keep it that way - it is one of only two
leaves in the set, and a leaf is what makes the rest of the dependency graph tractable.

In particular, do not relocate `RunProgramWait` (or the rest of `WsGlobalFunctions.pkg`) into
RDCToolsLib. `DfAbout.pkg` calls it for the signtool certificate display, so the move would give
this library its first dependency - on a library that itself depends on vwin32fh.

## Compiling it on its own

Not currently possible, and worth fixing if standalone verification matters here.
`DfAbout.pkg` unconditionally defines `ShouldEmbeddAboutHelpFile`, which enables an
`Include_Resource ..\Help\About.rtf`. That path assumes the usual `AppSrc\` + `Help\` sibling
layout of an application workspace. DFAbout's own `Config.ws` is flat (`Home=.`, `AppSrcPath=.`,
`HelpPath=.`), so `..\Help\About.rtf` resolves outside the library folder and does not exist.

Consumers are unaffected - their workspaces do have that layout, which is why this has never
shown up as a problem.
