# .NET Version Upgrade Plan

## Overview

**Target**: AsmSpyPlus solution → migrate projects from .NET Framework 4.8 to net10.0-windows
**Scope**: 1 Classic WinForms project (AsmSpyPlus.csproj), ~1k LOC, SDK-style conversion required; estimated moderate effort and manual code fixes for binary-incompatible APIs.

## Tasks

### 01-convert-to-sdk-style: Convert AsmSpyPlus.csproj to SDK-style

Convert the classic (non-SDK) AsmSpyPlus.csproj into an SDK-style project that targets net10.0-windows and enables UseWindowsDesktop. Preserve assembly name, resource files, and embedded manifests. Ensure project builds under the new SDK and resources are included.

**Done when**: The project file is an SDK-style MSBuild project targeting net10.0-windows, builds without errors, and the application launches (at least starts) on a developer machine.

---

### 02-update-target-framework-and-refs: Update Target Framework and project references

Update TargetFramework(s) to net10.0-windows, adjust any project reference metadata required by SDK-style projects, and update any conditional compilation symbols if necessary.

**Done when**: Project's TargetFramework is net10.0-windows and project references resolve and compile.

---

### 03-update-packages-and-config: Update NuGet packages and configuration

Restore, update, or add NuGet packages needed for net10.0-windows (e.g., System.Configuration.ConfigurationManager if required). Migrate legacy app.config usage to supported configuration patterns or add bridging packages as interim measures.

**Done when**: All required packages are referenced with compatible versions and configuration access works at runtime where exercised by unit/manual tests.

---

### 04-fix-compile-errors: Resolve compile-time API incompatibilities

Address source-incompatible and binary-incompatible API usages identified in assessment.md (e.g., reflection-only loads, ProcessorArchitecture usage). Replace or rework APIs to supported equivalents in .NET 10.

**Done when**: Solution compiles without errors and all previously failing projects build successfully.

---

### 05-run-tests-and-validate: Run tests and perform runtime validation

Run unit/integration tests (if present) and perform manual runtime checks of key scenarios to validate behavioral changes. Focus on UI flows, file/assembly loading, and configuration boundaries.

**Done when**: Tests pass and smoke verification steps complete without regressions.

---

### 06-finalize-and-cleanup: Finalize changes and prepare for merge

Clean up project files, remove temporary compatibility workarounds where appropriate, update documentation, and create PR with description of changes and known follow-ups.

**Done when**: PR is prepared on branch upgrade-dotnet-10 and tasks.md shows all tasks completed.

