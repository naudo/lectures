#Sublime Text notes

If you want to open all of the files in a directory (project) but don't
want to modify your alias when you add a new file, you can change your
subl call to just "subl ." (no quotes). The dot after subl tells it to
just load everything. Your command would then become:

````bash
alias pjt="cd ~/path your project/ &&  subl . &  || echo 'uh oh!!' "
````
Now after you do this there are a few hotkeys that you may not know
about. `Cmd-T` on mac `Ctrl-T` on linux(?). This is the Sublime fuzzy find.
Play around for a bit and notice how sublime doesn't care if words are
right next to each other. This is great for when you have a lot of
similarly named files. Additionally you probably know to use `Cmd +F` to
search a file (`Ctrl-F` on linux), but did you know that if you `Cmd + Shift + F`
that it will do a project wide search (default, you can play around with
filters and such for regex / case sensitive, etc).

You will probably notice after a while there are some files you just
don't care about  editing (ie your virtual env folder, images, etc) that
now show up in your sublime tray.  This can be annoying and will slow
down project wide search / mess with your search results.

Fortunately you can configure sublime pretty heavily. The settings file
is just json. Open the settings (Cmd + , on mac) and go ahead and add
what ever you want to the file under the folder_exclude_patterns entry.

Something like this.
````json
{
"font_size": 15.0,
"folder_exclude_patterns": ["ENV",    "*.min.js"]
}
````


It's a bit lacking, but here is some more info about thishe sublime
settings file if you're curious
http://www.sublimetext.com/docs/2/settings.html
