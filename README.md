
```
Usage: tailsince FILE

Tail a (log) file, showing lines since a given date, or since a period of time. With no
FILE, or when FILE is -, read standard input.

Options:
  -h, --help            show this help message and exit
  -p PERIOD, --period=PERIOD
                        period of time (defaults to "1d" or 1 day)
  -d DATE, --date=DATE  use a specified date instead of a period of time. this takes
                        precedence over -p
  -a, --append-patterns
                        append, rather than replace, default patterns with patterns from
                        ~/.tailsince

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
for parsing dates from the input.

Examples:

  # tail entries since last hour
  cat /var/log/apache/access.log | tailsince -p 1h

  # tail entries since 3 days, 6 hours
  tailsince -p 3d6h /var/log/apache/access.log

  # tail entries since 2pm today
  tailsince -d 14:00 /var/log/apache/access.log
  
```
