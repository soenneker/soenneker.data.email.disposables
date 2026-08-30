[![](https://img.shields.io/nuget/v/soenneker.data.email.disposables.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.data.email.disposables/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.data.email.disposables/build-and-test.yml?style=for-the-badge)](https://github.com/soenneker/soenneker.data.email.disposables/actions/workflows/build-and-test.yml)
[![](https://img.shields.io/nuget/dt/soenneker.data.email.disposables.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.data.email.disposables/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.data.email.disposables/codeql.yml?label=CodeQL&style=for-the-badge)](https://github.com/soenneker/soenneker.data.email.disposables/actions/workflows/codeql.yml)

# Soenneker.Data.Email.Disposables

A packaged newline-delimited list of domains associated with disposable or temporary email services.

## Installation

```bash
dotnet add package Soenneker.Data.Email.Disposables
```

The package copies this file to the consuming application's output directory:

```text
Resources/data-email-disposables.txt
```

It contains one domain per line. The package provides data only—there is no service, parser, validator, or dependency-injection registration.

## Load the domain set

```csharp
string path = Path.Combine(
    AppContext.BaseDirectory,
    "Resources",
    "data-email-disposables.txt");

HashSet<string> disposableDomains = File.ReadLines(path)
    .Select(static line => line.Trim())
    .Where(static line => line.Length > 0)
    .ToHashSet(StringComparer.OrdinalIgnoreCase);
```

Then compare a normalized domain, not the complete email address:

```csharp
string domain = "mailinator.com";
bool isDisposable = disposableDomains.Contains(domain.TrimEnd('.'));
```

Parse and validate email addresses before extracting their domain. Convert internationalized domain names to their ASCII/Punycode form when required by your input pipeline, and remove a terminal DNS dot before lookup.

## Operational guidance

The list is a snapshot shipped with the installed package version. Updating the NuGet package updates the output asset; an already deployed application does not download list changes at runtime.

Domain-list matching is heuristic. Providers appear, disappear, and change ownership, and legitimate domains can be listed accidentally. Use the result as one abuse signal rather than the sole reason to reject an account. Consider an override list and log decisions so false positives can be corrected.

Loading the file into a case-insensitive `HashSet<string>` provides fast repeated lookup at the cost of retaining the complete list in memory. For occasional checks, scanning the file or using a different indexed store may be more appropriate.
