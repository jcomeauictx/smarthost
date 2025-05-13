# smarthost

This project is for digital nomads who own their own servers for DNS and email,
and want to be able to set up their laptops to send email from the command line
using bsd-mailx, s-nail, or mailutils.

It assumes a Debian system with exim4; exim4-daemon-light is suitable for a
smarthost setup. You will likely want exim4-daemon-heavy on the mailserver
itself.

I've used other approaches over the years, including ssh tunneling and
nullmailer, and might someday document those. But this, while a little
complicated to set up, seems to be the most reliable of the 3.

These instructions are based on <https://wiki.debian.org/Exim>, and I highly
recommend at least skimming that page before continuing.
