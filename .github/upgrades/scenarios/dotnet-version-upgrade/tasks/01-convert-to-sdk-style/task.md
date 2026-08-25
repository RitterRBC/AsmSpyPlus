# 01-convert-to-sdk-style: Convert AsmSpyPlus.csproj to SDK-style

Convert the classic (non-SDK) AsmSpyPlus.csproj into an SDK-style project that targets net10.0-windows and enables UseWindowsDesktop. Preserve assembly name, resource files, and embedded manifests. Ensure project builds under the new SDK and resources are included.

**Done when**: The project file is an SDK-style MSBuild project targeting net10.0-windows, builds without errors, and the application launches (at least starts) on a developer machine.
