mutt-ical.py is meant as a simple way to reply to display and reply to ical invitations from mutt.

It was originally authored by Martin Sander, and later modified by Dominic White.

Installing
----------

1) Copy it into somewhere in your PATH, (or you can specify the PATH in your .mailcap)
2) Edit your mailcap (~/.mailcap or /etc/mailcap) to have the following line:

    text/calendar; <path>mutt-ical.py -i -e "user@domain.tld" %s
    application/ics; <path>mutt-ical.py -i -e "user@domain.tld" %s

(Don't forget to add your email address)

OSX Users
---------

3) For added fun on OSX, you can extend it to the following, to get iCal to open it nicely too (iCal cares not for mime types it seems):

    text/calendar; mv %s %s.ics && open %s.ics && <path>mutt-ical.py -i -e "user@domain.tld" %s.ics && rm %s.ics

4) You can force iCal to stop trying to send mail on your behalf by replacing the file /Applications/iCal.app/Contents/Resources/Scripts/Mail.scpt with your own ActionScript. I went with the following: error number -128 Which tells it that the user cancelled the action.

    i) Open AppleScript Editor, paste the code from above into a new script, then save it.
    ii) Move the old script /Applications/iCal.app/Contents/Resources/Scripts/Mail.scpt just in case you want to re-enable the functionality.
    iii) Copy your new script into place.

Usage
-----

To reply, just open the ical file from mutt by:
	i) Viewing the attachements (usually 'v')
	ii) Invoking the mailcap entry (usually 'm')
	iii) Choosing your reply

Martin also included the sendmail wrapper, but since mutt's SMTP support has now improved, rather configure your SMTP settings through mutt's config. The wrapper is kept in case someone finds it useful. However, the get_mutt_command function will need the relevant code uncommented to use it.

Requirements
------------

mutt, python, bash, vobject:
http://vobject.skyhouseconsulting.com/ or 'easy_install vobject'

Inspired by:
    http://weirdzone.ru/~veider/accept.py
    http://vpim.rubyforge.org/files/samples/README_mutt.html
