# [Welcome](https://tryhackme.com/room/welcome)

**Tip:** Complete the [OpenVPN room](https://tryhackme.com/room/openvpn) or follow this [guide](https://tryhackme.com/access?t=vpn) to access OpenVPN

---

This room focuses on the idea of machines, these are virtualized services, virtualized operating systems, and virtualized hardware that all run on a server.
During your learning at THM you will often connect to different machines, most of them being vulnerable to attacks with the aim of gaining knowledge of its mechanisms.

#### Scripting

The script [getflag.sh](getflag.sh) is a simple way to access a website and retrieve the flag text shown on the webpage using the commands `curl`, `grep` and `echo`.

To use the script, you need to provide the IP address of the machine as an argument when running the script. For example:

`./script.sh 10.10.63.99`

This will retrieve the webpage at `http://10.10.63.99` and print the flag text if it's found.

<br>

**Note:** this script is just an automated solution, you're also able to find the flag by simply opening the website in a browser and searching for it.

To get help with Linux commands, you can use the following:

- `man` command (e.g. `man ls`) to access command manual pages,
- `--help` option (e.g. `ls --help`) to see command options and usage,
- Google it, it is your friend.
