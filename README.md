battery
=======

A Bash program to print your Linux machine's battery level.

1. [Download](#download)
2. [Use](#use)
3. [Example output](#example-output)
4. [Exit codes](#exit-codes)
5. [How it works](#how-it-works)
6. [Why I made this](#why-i-made-this)
7. [License](#license)

Download
--------

```shell
curl -O https://cszach.github.io/battery/battery
chmod +x battery
mv battery ~/.local/bin  # Optional
```

Use
---

#### Get help

```shell
battery --help
```

#### Print the battery level

```shell
battery
```

#### Print the battery level of `BAT1`

```shell
battery BAT1
```

#### List batteries and power supplies

```shell
battery --list
```

#### Print the battery level and colorize

```shell
battery --color=always
```

#### Print the battery level of `BAT1` and colorize only if it is charging

```shell
battery --color=charging BAT1
```

Example output
--------------

```
75%
```

Exit codes
----------

```shell
echo $?
```

- `0`: Successful.
- `1`: Invalid option.
- `2`: Battery could not be found.
- `3`: Battery's level could not be accessed.

How it works
------------

- Power supplies are found in `/sys/class/power_supply`.
- The battery level is found in `/sys/class/power_supply/BATTERY/capacity` where
  `BATTERY` is a power source detected by your Linux system.
- The charging state is found in `/sys/class/power_supply/BATTERY/status`. The
  content of this file is either `Charging`, `Discharging`, `Full`, or
  `Unknown`.

Why I made this
---------------

I didn't want to use a graphical desktop on my [Parabola GNU/Linux-libre][para]
laptop so I needed a way to know the battery level in the command line. I wanted
the output to be colorized, too (e.g. green for good battery level, red for weak
battery), so it was more than just a one-liner. Ultimately, I figured out I
could share this little Bash script with the Internet, so I decided to support
user-given power source and push this onto GitHub.

You can easily integrate this program with your `PS1` command prompt, like this:

```shell
# ~/.bashrc

PS1="$(battery) $"
```

[para]: https://parabola.nu

License
-------

This work is licensed under the [Creative Commons Zero v1.0 Universal][license]
and is therefore a dedication to the public domain. This means you can copy,
modify, and redistribute the program without asking for permission.

[license]: https://creativecommons.org/publicdomain/zero/1.0
