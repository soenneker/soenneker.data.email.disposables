[![](https://img.shields.io/nuget/v/soenneker.data.email.disposables.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.data.email.disposables/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.data.email.disposables/build-and-test.yml?style=for-the-badge)](https://github.com/soenneker/soenneker.data.email.disposables/actions/workflows/build-and-test.yml)
[![](https://img.shields.io/nuget/dt/soenneker.data.email.disposables.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.data.email.disposables/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.data.email.disposables/codeql.yml?label=CodeQL&style=for-the-badge)](https://github.com/soenneker/soenneker.data.email.disposables/actions/workflows/codeql.yml)

# Soenneker.Data.Email.Disposables

Simply adds a list of compiled disposable/temporary email domains, updated daily (if available).

## Install

```bash
dotnet add package Soenneker.Data.Email.Disposables
```

## What it provides

- Simply adds a list of compiled disposable/temporary email domains, updated daily (if available).
- The file is copied to the output directory, and located at the relative path: `Resources\data-email-disposables.txt`.

## How to use it

After installation, resolve the packaged file from the output-relative path above. The package deploys the asset but does not invoke it for you.
