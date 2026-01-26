Display Managers in [[Unix]] and [[Linux]] environments are **software that runs before you log in** into a graphical environment.
Their job is to **start the graphical server ([[X11]] or [[Wayland]]), present the login screen, authenticate you and then hand you off to your session**.
# Launching a Window Manager
When you log in through a display manager, **it looks through `/usr/share/wayland-sessions` (or `/usr/share/xsessions` for `.desktop` files**.
It then reads instructions inside of those files to know what command to launch, and thus, a session is born (and you're dropped into Kwin, Gnome or whatever [[Window Manager]] you setup).