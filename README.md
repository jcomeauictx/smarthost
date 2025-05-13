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

1. First edit the smarthost.patch file, replacing:
  * all instances of `klughost` with the hostname of your mailserver
  * all instances of `devbox` with the hostname of your laptop
  * all instances of `example.net` with your domain name
2. Patch the exim4 configuration
  * `cd /etc`
  * `sudo cp -r exim4 exim4.dpkg.orig`  # save a copy of standard config
  * `sudo patch -p0 < ~/path/to/modified/smarthost.patch`
3. Then, on your DNS server, edit /etc/bind/local/db.example.net (of course
  with your own domainname here) and add SPF and DKIM records for your
  devbox:
  * `devbox IN TXT "v=spf1 ip4:172.30.43.79 include:yahoo.com ?all"`
  * `default._domainkey.devbox IN TXT "k=rsa; t=s; p=L0NgA55str1nGg03sH3R3"`
  Again, of course, replacing the hostnames and strings with what you have
  for the rest of your domain's entries.
4. Restart the services
  * `sudo systemctl restart exim4` on devbox
  * `sudo systemctl restart bind9` on the DNS server

That should be it. I don't remember having to do anything on the mailserver
at all, other than set up the `klugmann` account.
