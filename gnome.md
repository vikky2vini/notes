## GNOME

#### Misc fixes
Fix Locale Issues/Errors:
	1. # locale-gen
	2. # localectl set-locale LANG="en_US.UTF-8"

Fix tracker:
	1. $ rm -rf ~/.cache/tracker
	2. $ rm -rf ~/.config/tracker/
	3. $ rm -rf ~/.local/share/tracker/
	4. $ tracker-control -r
	5. $ tracker-control -s
