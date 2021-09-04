# Windows TZ strings

For [PerlPowerTools](https://perlpowertools.com), I want to map the Windows names for the timezones to the common abbreviations we see in the Unix `date` command:

	$ date
	Sat Sep  4 08:11:58 EDT 2021

In a POSIX system or something using the Olson locations, figuring out the timezone abbreviations are trivial because there are APIs for this. For example, POSIX's `strftime` can use `%Z`.

	$ perl -MPOSIX -le 'print strftime "%Z", localtime'
	EDT

	$ perl -MPOSIX -le 'print strftime "%z", localtime'
	-0400

Windows is not so easy (or I couldn't find the easy way to do this) because they don't deal with those abbreviations (or the Olson locations).

The strings I need to map depend on the language pack. I've done a few
languages, but some we leave the Latin alphabet, I have problems.

## Adding to the project

The best thing to send me is the output of this PowerShell cmdlet:

	PS C:\> Get-TimeZone -ListAvailable

I'll take data any way that you want to transmit it. Email (brian.d.foy@gmail.com), [pastebin](https://pastebin.com),
[gist](https://gist.github.com), or, preferably, a [pull request](https://github.com/briandfoy/windows-tz-strings/pulls).

For a pull request, make a new file with a name that represents your
language pack. Leave a few comments to explain anything I may need to
now.

## Next steps

Eventually I will collate all of this information into some sort of language-agnostic data file that anything can consume. I haven't thought that far yet.



