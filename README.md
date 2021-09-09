# Windows TZ strings

For [PerlPowerTools](https://perlpowertools.com), I want to map the Windows names for the timezones to the common abbreviations we see in the Unix `date` command:

	$ date
	Sat Sep  4 08:11:58 EDT 2021

In a POSIX system or something using the Olson locations, figuring out the timezone abbreviations are trivial because there are APIs for this. For example, POSIX's `strftime` can use `%Z`.

	$ perl -MPOSIX -le 'print strftime "%Z", localtime'
	EDT

	$ perl -MPOSIX -le 'print strftime "%z", localtime'
	-0400

Windows is not so easy (or I couldn't find the easy way to do this) because they don't deal with those abbreviations (or the Olson locations). Consider the many StackOverflow answers in [Display current time with time zone in PowerShell](https://stackoverflow.com/q/11035905/2766176).

The strings I need to map depend on the language pack. I've done a few
languages, but some we leave the Latin alphabet, I have problems with the keyboard and typing out characters to run a command

But, Windows does have IDs for each of the time zones, which appear to be invariant across language packs:

	PS C:\Users\brian d foy> Get-TimeZone | Select-Object -expandproperty Id

That might be enough to map everything, but I'm curious if not only are those IDs the same, but if different language packs have additional IDs. I imagine there are some political problems with recognizing certain timezones.

## Adding to the project

The best thing to send me is the output of this PowerShell cmdlet, substituting the right values for `lang` and `COUNTRY`:

    PS C:\Users\brian d foy> Get-TimeZone -ListAvailable > lang-COUNTRY.txt

If you'd like to send a pull request (and get some internet points), fork the repo, clone it, and add your data. Be sure to use the UTF-8 code page (65001):

    PS C:\Users\brian d foy> chcp 65001
    PS C:\Users\brian d foy> git clone git://github.com/YOUR_GITHUB_NAME/windows-tz-strings
    PS C:\Users\brian d foy> cd windows-tz-strings/outputs
    PS C:\Users\brian d foy> Get-TimeZone -ListAvailable > lang-COUNTRY.txt
    PS C:\Users\brian d foy> git add lang-COUNTRY.txt
    PS C:\Users\brian d foy> git commit -m "Get-TimeZone for lang-COUNTRY" lang-COUNTRY.txt
    PS C:\Users\brian d foy> git push origin master

Then go to your fork and make the pull request.

If that's too much work, I'll take data any way that you want to transmit it. Email (brian.d.foy@gmail.com), [pastebin](https://pastebin.com),
[gist](https://gist.github.com), or whatever.

## Next steps

Eventually I will collate all of this information into some sort of language-agnostic data file that anything can consume. I haven't thought that far yet.

## Other notes

Extracting the Timezone ID, which I think is invariant across language packs:

	PS> Get-TimeZone | Select-Object -expandproperty Id

