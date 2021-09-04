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
languages, but some we leave the Latin alphabet, I have problems with the keyboard and typing out characters to run a command

## Adding to the project

The best thing to send me is the output of this PowerShell cmdlet:

	PS C:\Users\brian d foy> Get-TimeZone -ListAvailable > lang-COUNTRY.txt

If you'd like to send a pull request (and get some internet points), fork the repo, clone it, and add your data:

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



