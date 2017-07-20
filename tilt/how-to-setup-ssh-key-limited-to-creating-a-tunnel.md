# How to Setup SSH Key limited to Creating a Tunnel

For a given key I was intending to prevent **any** interaction **except** for starting an SSH tunnel to a particular local port. Turns out that for each key in `~/.ssh/authorized_keys` you can add so called *login options*, buy preppending them to the key, like that:

    option="value",option-without-value,another-option <KEY ...> <COMMENT>

This combination of options seem to do the trick:

    command="",restrict,port-forwarding,permitopen="localhost:80"

Let me go through each of them individually:

- `command=""`

  disallows any command to be executed using this key

- `restrict`

  Disable all options, such as TTY allocation, port forwarding, agent forwarding, user-rc, and X11 forwarding all at once.

- `port-forwarding`

  Enables TCP port forwarding, but see below.

- `permitopen="localhost:80"`

  Limits TCP port forwarding to local port `80`. That's the **only** thing this key should allow.

So in total it's:


    command="",restrict,port-forwarding,permitopen="localhost:80" ssh-rsa AAAAB3NzaC1yc2EAAA[...]3c7rmJT5/ tunnel@a.example.com

Make sure it's all in one line and there are is no whitespace between the options.

I've been able to figure this out mainly by reading [Client Configuration Files chapter of OpenSSH WikiBook](https://en.wikibooks.org/wiki/OpenSSH/Client_Configuration_Files), so the majority of credit goes to it's authors (Lars Noodén et al.). Missing part was `port-forwarding` - without it forwarding is forbidden even though `permitopen` would suggest otherwise.

Here is some more background: https://superuser.com/a/1231232/195460
