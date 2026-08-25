# Upgrade Options for AsmSpyPlus

Generated from assessment: assessment.md

## Summary Recommendation
- Target Framework: net10.0-windows (LTS)
- Upgrade Strategy: Convert project to SDK-style (Microsoft.NET.Sdk or Microsoft.NET.Sdk.WindowsDesktop) then migrate API usages and fix incompatibilities. Prioritize creating a working SDK-style project that sets <UseWindowsDesktop>true</UseWindowsDesktop> and targets net10.0-windows.
- Complexity: Complex — many binary-incompatible APIs detected; estimated ~10% LOC impact; SDK-style conversion required.

## Options Evaluated
1. net8.0 (LTS)
   - Pros: LTS, earlier stable Windows desktop support
   - Cons: older than net10.0; similar migration work required
2. net9.0 (STS)
   - Pros: may require less initial changes for Windows desktop in some APIs
   - Cons: STS (short-term support), not recommended for long-term
3. net10.0 (LTS) — Recommended
   - Pros: LTS, newest stable features, recommended by default
   - Cons: Requires same SDK-style conversion and code fixes; some behavioral changes to validate

## Strategy Details
- Phase 1: Create SDK-style project file for AsmSpyPlus.csproj targeting net10.0-windows and enable UseWindowsDesktop. Preserve existing assembly name and resources. Commit as new branch: upgrade-dotnet-10.
- Phase 2: Restore and update NuGet packages as needed (none detected in assessment), add System.Configuration.ConfigurationManager if needed for legacy config support.
- Phase 3: Compile and resolve source-incompatible APIs, fix binary-incompatible usages, and run tests/manual verification.
- Phase 4: Validate runtime behavior, update documentation, finalize changes.

## Preconditions / Notes
- Project is Classic WinForms (non-SDK) targeting net48. SDK-style conversion is required and likely the largest change.
- Assessment flagged many binary-incompatible APIs; expect manual code fixes.

## Generated for orchestrator
- Recommended targetFramework: net10.0-windows
- Recommended working branch: upgrade-dotnet-10
- Recommended upgradeStrategy: sdk-style-conversion-then-migrate

