# fprintd en_US Prompt Override

An Arch Linux package that changes this `pam_fprintd` prompt:

```text
Place your right index finger on the fingerprint reader
```

to:

```text
Touch the fingerprint reader
```

The package installs an `en_US` gettext catalog. It does not replace
`pam_fprintd.so`, change fingerprint selection, or modify authentication logic.

## Requirements

- Arch Linux
- `fprintd`
- An `en_US.UTF-8` message locale in the application invoking PAM
- The standard Arch package build tools

## Build

Review `PKGBUILD` and `fprintd.po`, then build the package:

```bash
makepkg -f
```

Building does not install anything or require root privileges. The resulting
package is:

```text
fprintd-en-us-prompt-override-1-1-any.pkg.tar.zst
```

## Inspect

List the files that the package would install:

```bash
pacman -Qlp fprintd-en-us-prompt-override-1-1-any.pkg.tar.zst
```

The only payload should be:

```text
/usr/share/locale/en_US/LC_MESSAGES/fprintd.mo
```

Inspect the compiled message catalog:

```bash
msgunfmt src/fprintd.mo
```

## Install

Install the built package with Pacman:

```bash
sudo pacman -U ./fprintd-en-us-prompt-override-1-1-any.pkg.tar.zst
```

Log out and back in before testing the prompt. Gettext intentionally ignores
translation catalogs when the PAM application uses the `C` or `POSIX` locale.

## Customize

Edit the replacement in `fprintd.po`. Keep the `msgid` unchanged because it is
the lookup key used by `pam_fprintd`; change only `msgstr`.

After editing the catalog, generate its new checksum:

```bash
makepkg -g
```

Replace the `sha256sums` value in `PKGBUILD` with the generated value, then
rebuild:

```bash
makepkg -f
```

## Remove

```bash
sudo pacman -Rns fprintd-en-us-prompt-override
```

Removing the package removes the custom catalog, so gettext falls back to the
original message built into `pam_fprintd`.

## Compatibility

The override matches an exact upstream English `msgid`. If fprintd changes that
source message in a future release, authentication will continue to work, but
the original upstream wording will be displayed until `fprintd.po` is updated.
