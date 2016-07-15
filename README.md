
tailsince
=========

Tail a (log) file, showing lines since a given timestamp or period of
time.

Requirements
------------

You'll need to have Python 2.7+ installed. Compatible with Python 3.

Installation
------------

- Clone or download this repository.

- Make sure the file `tailsince` is executable by all, and move it to
  a bin directory in your path. `/usr/local/bin` is a good choice.
  
  ```
  chmod 0755 tailsince
  sudo cp tailsince /usr/local/bin
  ```

- You should now be able to run `tailsince` anywhere.

Usage
-----

Here is the output of `tailsince -h`:

```
Usage: tailsince FILE

Tail a (log) file, showing lines since a given timestamp or period of
time. With no FILE, or when FILE is -, read standard input.

Options:
  -h, --help            show this help message and exit
  -p PERIOD, --period=PERIOD
                        period of time (defaults to "1d" or 1 day)
  -d DATE, --date=DATE  use a specified date instead of a period of time. this
                        takes precedence over -p
  -n NUM_LINES, --start-num-lines-from-end=NUM_LINES
                        start searching n lines from end of file
  -a, --append-patterns
                        append, rather than replace, default patterns with
                        patterns from ~/.tailsince

PERIOD is a string without whitespace representing a time period. Examples:

  1w = 1 week
  2d = 2 days
  3h = 3 hours
  4m = 4 minutes
  5s = 5 seconds
  2d12h = 2 days and 12 hours

DATE is a string without whitespace representing a date. The format MUST be
one of the following:

  YYYY-MM-DD
  YYYY-MM-DD:HH:MM
  HH:MM (current date is assumed)

You may optionally create a ~/.tailsince file to list regexes, one per line,
for parsing timestamps from the input.

Examples:

  # tail entries since last hour
  tailsince -p 1h < /var/log/apache/access.log

  # tail entries since 3 days, 6 hours
  tailsince -p 3d6h /var/log/apache/access.log

  # tail entries since 2pm today
  tailsince -d 14:00 /var/log/apache/access.log

  # tail entries since 2pm today, starting at 5,000 lines from EOF
  # (useful for very large files)
  tailsince -n 5000 -d 14:00 /var/log/apache/access.log
  
```

Customizing timestamp parsing
-----------------------------

You may optionally create a ~/.tailsince file to list regexes, one per
line, for parsing timestamps from the input. This lets you use
tailsince for log files that use any timestamp format.

Regex patterns can return these named groups: "year", "month", "day",
"hour", "minute", "second". month is handled as a special case, where
the parsed value can be a digit, a 3-letter month abbreviation
(e.g. "Jul") or a fully spelled out month name.

For example, here's the regex for parsing Apache log timestamps:

```
(?P<day>\d{2})/(?P<month>\w{3})/(?P<year>\d{4}):(?P<hour>\d{2}):(?P<minute>\d{2}):(?P<second>\d{2})
```
