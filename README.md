# Search and Destroy v3.0 (rel-1.0.6) — 4 Aug 2019
Good morning friends, ninjas, and other fellow associates.  This isn't much of an update, but it's here because I said I'd continue to work on and maintain S&D, and I told Lasher basically the same via email.  Regardless of what you may think of me, I'm not doing myself any favors if I don't follow through.

 - Fixed a crash occurring when your quest mob is 'missing'.
 - If your quest mob is missing, 'xq' will show its last known location.
 - I've had this feature on my own S&D for a while, "xcp next" when you kill your cp or gq mob.  Instead of having to 'xcp' the next mob every single time, now you don't.  The command 'xcp next' toggles the feature on and off, so you can use it or not as you see fit.
 - The mob keyword guesser now has an exceptions table which is currently part of the code, but which could easily be
 stored in and loaded from a separate .lua file.  The list of exceptions is far, far from complete but I had it in my own S&D so as proof of concept what I have is included with this update.  I'll go ahead and update it in the code for now, but just so you know my plan of action is to bring it in as part of the planned SDDB system, or to keep it up to date as a separate file that could be loaded in.
 
It's a short list but don't doubt me.  The next big thing is to assimilate the main features of Pwar's Winklegold, which means a lot of database stuff.  It's less complicated than I initially feared, and since Pwar 'borrowed' code from this S&D to use in Winklegold (which is fine, because you're allowed to copy and use what you want) I don't feel too bad about borrowing in return :)  I do plan on including a feature that will take a Winklegold database and copy its data to SDDB and have it work.  I just need some time to research some things and do the overall design work, and the main difficulty is time rather than anything technical.

That's it for now.  Full ahead and full speed.


# Search and Destroy v3.0 (rel-1.0.5) — 11 Apr 2019
Here is the latest update.  As with the last few, it's mainly bugfixes and similar.  Let me know what you think.

 - Fixed a crash occuring when running to a vidblain location while on a room cp.
 - Mob keyword guesser should correcly handle mob names like "Starling, the real ninja".
 - Apostrophes mid-mobname (e.g. in "gan'arg") are now removed from mob names.
 - Replaced "execute" function calls with the direct function for commands, e.g. xrun_to("", "", {destination="academy"}) instead of Execute("xrt academy").  Execute is quite slow, so calling the functions directly should improve speed/crispness a bit.
 - The mob in Necromancer's Guild "head necromancer's assistant" will always be targeted with its exact keywords "old mage assistant".  This change is the direct result of the recent shit show debate on typos board.  Some others disagree that this change is needed, but as it happens, good news: I have more control than they do—so, I say it gets changed.

Since taking over S&D, an increasingly common problem I encounter is that anytime I post a typos note suggesting that a keyword should be added to a mob (because the mob is missing that keyword), people immediately assume I want the keyword added so that S&D's mob name guesser can handle it properly.  That is not, in fact, why I suggest adding keywords to mobs; it has nothing to do with S&D.  To demonstrate this, I added mob keyword exceptions to prove how easy it is to simply add mobs and correct keywords to the exceptions table and have S&D handle them that way.  It isn't necessary to report missing keywords for S&D's benefit.  From where I'm sitting, people like to use S&D as a justification to be obtuse and/or not fix anything "because challenge", so now that I don't need to report missing keywords, I guess they get to complain about this instead.

Keep on keeping on, ninjas.  If there are any bugs or problems with this update please let me know.  Thanks for all your support!

# Search and Destroy v3.0 (rel-1.0.4) — 24 Mar 2019
Bit of a fast turn around, but the last update had some issues I wanted to clear up, and as usual I was able to find some other things to work on as well.  At this point we're scraping the bottom of the barrel as far as adding new features goes, which is why the update notes have been a lot less exciting lately.  Here are today's changes:

 - "Xcp", "go", and "nx" will no longer work while you're fighting, running, or otherwise occupied.  They're only useful 
 if you're standing, not running, and out of combat.  Outside of that, they would basically just send spam that slows you down 
 (and possibly looks silly to anyone who might be watching).  Now they just give a brief error message.
 
 - The window link for your current mob is supposed to grey out on mob kill and disappear when the next cp or gq check arrives,
 but, sometimes the xcp index would get lost. ("xcp 0", etc.)  In that case it would crash due to indexing a nil table item. 
 It should now be fixed.
 
 - I made the window layout a bit more compact and also changed the right side buttons a bit.  Hta and Clr are removed and replaced with Qw and Ht.  The Ref button is still the same and I don't know if I'm going to do anything with it yet.  I really
want to overhaul the button layout so that more buttons will fit, but unsure of how to proceed.  Suggestions, anyone?
 
 - Room cp's filter results based on areas' level ranges, but the stated levels range from kind-of ok, to fairly inaccurate, to
 flat-out wrong.  For example, Aylor Academy is stated as 1 to 100.  But, it's mostly inaccessible after level 10, so obviously
 level 100 is wrong.  In this case, the wrong level info resulted in level 80+ cp's generating useless links to Academy.  Most
 area level ranges aren't nearly as fixable as this one, which needed a simple if check and nothing else.  I'll look at
 mobdeath/mobquest level data and adjust what I can, but dozens of areas have level ranges that are too far off, or just too
 broad (although technically correct) to be used as filtering criteria.
 
 - Room gq's now use the gquest level range for filtering.  Before this, room gq's would use your current level, which worked well enough but was technically wrong.  Let me know if this causes any problems for you.
 
 - More than half of the files loaded via "require" (at the beginning of the plugin's Lua section) were never referenced by
 anything, so I removed them.
 
As always, if anything gives trouble, let me know.  We're really scraping the bottom of the barrel as far as finding more things to work on; most of S&D has been rewritten and the major bugs all fixed.  I still want to redo area level filtering, and I feel like the window design could be redone to make the button interface more compact and easier to use.  Any suggestions or ideas on any of this, or if anything new should be added, let me know.

Have a good one and I will see you next time!

# Search and Destroy v3.0 (rel-1.0.3) — 14 Mar 2019 
Good morning friends, ninjas, and everyone else, here are the latest updates and problem fixes:

 - Fixed the various issues with 'xcp' and 'xset vidblain'.  Depending on the situation, it could fail by not resuming speedwalk after passing through the dark portal, or by not doing qw/ht on arrival at the destination.  It should work correctly now but be on the lookout just in case.  Writing this was an adventure, to say the least.
 
 - 'xset vidblain level' with no argument now shows your vidblain portal level.
 
 - When a gq target requires multiple copies of a mob, the quantity numbers will update as they're killed, but gq check / target data will only update after you kill the last one.  The copies are usually near each other, so it makes sense to have 'xcp' retain its target and not delay things with unnecessary gq checks.
 
 - Added a filter to deal with room names that include color codes.  The codes were being included in GMCP output and would occasionally interfere with things.
 
 - I added a command 'xset roomhist' which shows the last 200 rooms you've been in, with your current room being item 0.  It's not fleshed out and doesn't do anything else, but if anyone can suggest uses for it let me know.
 
 - The rest is the usual reworking of messy code, including my own earlier at this point, aimed at cutting things down and removing potential for errors as much as possible.
 
The discussion on gquest and whatnot is happening on the ideas board as we speak, so if you're one of the dozens who have sent me messages about how S&D has been a positive thing for you, now would be the time to post that.  Most of the feedback is coming from people who don't use S&D (currently, or at all), so it should be clear enough who knows what they're talking about, who is a Luddite, etc.  Seriously, if you like S&D please go post something about it.  Who knows where all of it will land, but for now enjoy the update and let me know if it acts up at all.

# Search and Destroy v3.0 (rel-1.0.2) — 21 Feb 2019
The update to S&D v3.0 is as follows:

- Improved 'where' handling, especially where quick-where is concerned.  This will be most apparent in areas like FTII.  Basically, it will look for an exact match to your cp/gq mob and loop through 'where' until it finds it or quits due to hitting 100.mob, whichever happens first.

- Rewrote execute_in_area from scratch, improving this most necessary of systems.

- Reorganized a bunch of stuff pertaining to window refreshing, aimed at cutting some lag out of the overall process.  In particular, the action button draw routines were re-written from scratch.

- Tightened overall gquest tracking and related things.

- In gquest, the output window will have quantity indicators of the form n\*mobname.

When you look at it like that it doesn't really look like much of an update, but from the standpoint of effort invested and hassle incurred it most definitely is.  One thing I should like to clear up, just in case, is that S&D 3.0 is aimed more at providing gq capability "at all", as contrasted with what one might call "gquest superiority".  It handles gquest exactly as it handles campaigns, and as anyone with experience knows, proper area knowledge absolutely is essential; and relying on S&D to know everything for you will be prone (indeed, doomed) to failure.

I wish you good fortune in the wars to come, ninjas.  Full ahead and full speed.

# Search and Destroy v3.0 (rel-1.0.1) — 26 Jan 2019
Fixed multiple issues with gquest.  Special thanks to a friend:  You know who you are, and my gratitude goes with you.  Thanks  for the problem reports and generally bearing me while I nailed it all down.

For everyone else, the point is:  Gquest is working great.  The only minor update would be some sort of quantity indicator since gquest mobs are usually in multiples rather than just one, in contrast to campaigns.  But for that, S&D gquest does it baller like Rodman.  But, without most of the crazy, I hope.

Stay tuned, ninjas.  And warriors too (even you, RoqueWarrior).  The engines are started, running, and accelerating to full operational power.  Three, two, one, *now*:  Light up the reheat and takeoff!

Full ahead and full speed!

# Search and Destroy v3.0 (rel-1.0.0) — 1 Jan 2019
Note: Make sure to uninstall version 2.  Version 3 uses a different plugin id, so it's possible to have both installed at once.  

As a result of Lasher and the Immortals forking and hosting version 2, I am releasing a new, third version to make clear the distinction between *this* project and whatever else exists.  Version 2 was the best of all of them, and this version is already better than that.  S&D is literally better than itself.

Happy 2019.  Welcome to version 3.

# Search and Destroy v2.0 (rel-1.0.9) — 24 Dec 2018
 - S&D now supports gquest and as of 30 Dec it finally works.  All you have to do is join a gq, wait for it to start, and then type 'gq info' to load target data and detect if it's an area or room gq.  From there it handles like a cp.  You can be on a gq and cp at the same time - 'cp check' and 'gq check' will change between cp and gq mob lists.  Xcp, go, and so on are used for both.  The implementation is a new design and isn't based on prior gq S&D or other scripts.

If there are any problems, email them to me.  

Other changes:

 - Updated the noexp indicator in the GUI window, apparently it was "weird" before but should look better now.  If noexp is on, the arrow will be red with a double red crossbar at top.  If noexp is off the arrow will be grey with a single green crossbar at top.
 
 - I gave the cp level indicator and noexp cutoff readout a sort-of "relief" or "depth" effect similar to how the numbers in MMORPG's look.  I think it looks ok, and is an interesting concept in plugin graphical design.
 
The change list is short, but gquest support is significant for being the #1 most-requested feature.  I got more requests for gquest than all other feature requests combined, from old and new players alike, and from all walks of Aard life.  A mob database was #2, a distant second.

Lastly, "gq hist" shows a lot of no-winner gquests, even in the 200+ bracket.  Go win some of them.

# Search and Destroy v2.0 (rel-1.0.7) — 15 Oct 2018
Good morning, this S&D update is mostly internal code changes, fixes, and things like that.  I'm too tired to think of anything witty to say at the moment, so here's what's new:

 - I rewrote the mob keyword guessing process from scratch due to intractable problems with the original.  The new version can filter things like 'dragon whelp' in Hatchling Aerie.  That and similar situations should be a lot better now.  It's still possible to guess wrong, but the improved filtering makes it less likely.  As a 'bonus' the mob keywords will randomly vary in length, from 4 to 5 characters for double keywords, and somewhat more so for single-keyword mobs.  I was bored.

 - Mob keywords, mob link color, and similar are now determined earlier in the process that starts with cp check and ends with  nicely displayed target info.  Previously, it was done during the process that builds and displays the text links in the main window.  Moving it to the target list builder's database loop makes it easier to maintain and the altered timing seems to reduce display lag a bit.

 - Quick where has also been rewritten.  It was overly complicated and had some long-standing issues.  Most of the complexity came from the fact that quick where can be called manually or by script, and the approach that was taken to deal with that.  It was too convoluted and difficult to follow, so I fixed that.  Also, the new version sort-of checks to see if the 'where' output is just flat-out wrong.  For example, if I want to look for "a villager" I probably don't want info for "a confused shopper" but they both have villager as a keyword.  If the output is obviously wrong it will try 2.villager and so forth.  It can still get the wrong mob (e.g. "a confused villager" or similar) but if totally wrong it should be able to skip it and try the next.

 - Quick where will no longer guess mob keywords when called manually.

 - The glitchiness with moving and resizing the GUI window should be mostly fixed.  I'm sure I missed something and it's still possible to bug it out, but for the most part it moves and handles like other plugins, and should no longer "jump" when you grab the title bar.
 
 - There are improvements to the GUI window, mainly dealing with the cp level readout.  Red means you must level before taking a new cp, green means you can take a new cp at your current level, and blue means the plugin is installing or you are offline.  I also cleaned up a lot of its code in general and I think it works pretty well now.
 
 - The process used to determine when you have arrived in the correct zone (area cp's) has been revamped and is faster.
 
 - Improved output when using 'xq' to target your quest mob, and improved quest status tracking.
 
 - I adjusted the level filtering in room cp's again.  This is just something that can't be gotten perfect simply by using the game-defined area level limits.  For example, living wall is level 86, but it's in an area with a level max of 55, so it will show as "ignoring due to level".  The aim here is to reduce the number of links which can sometimes be excessive ("the kitchen" exists in more than a dozen areas) but for now it's a trade-off between having a sensible number of links and getting it right enough of the time.  In most room cp's it isn't a big problem, and there are few enough of these that I can probably do an area-specific filtering thing similar to that found in the keyword guesser.
 
 - On that topic, the "ignoring due to level" messages are in red so as to be more visible.
 
 - Also regarding room cp's, fixed a crash in the cp target builder involving 'noquest' areas.
 
 - I tightened up a lot of the regexp regarding trigger matches, avoiding some accidental triggering and issues arising if the trigger fires on text that is somehow toxic to the plugin.  It seldom happened anyway, and in general was a random fluke when it did, mainly being possible when reading notes and in similar situations.  It should be very unlikely now.

I'm a little nervous about this update due to the number of changes and won't be too surprised if there are error reports, but as usual just let me know about them and I'll fix them as soon as I can.  Thanks for all your ongoing support!

# Search and Destroy v2.0.0 — 19 Aug 2018
Good morning, it's time once again to turn the thermostat of awesome up a notch and so here we are.  Thanks to everyone for reporting issues with the beta and helping me find the root cause of those problems.  At this point the issues arising from the three-plugin system are basically gone.  Most of these came down to lots of duplicate (triplicate, really) code, issues with plugin broadcast and response, and issues when a change to one plugin breaks the others (which I must then fix).  The merge went a lot smoother than I expected and the number of problem reports dropped off fast as things were fixed.

The beta is therefore finished and v2.0.0 is officially live.  The main feature is the merge itself rather than any actual new things, but there are some other improvements as well:

 - Removing the plugin-broadcast system fixed all of the data sync issues and having to track a lot of changes across all three files.
 
 - Removing all the duplicate code makes it run smoother and without the laggy feel it used to have.
 
 - Everything in one file makes changes and whatnot much more predictable, avoiding problems and saving time.
 
 - At SH, the messages about being able to take a new campaign are different from when you are levelling.  This was overlooked in the original and I didn't catch it because I very seldom sit SH.  These messages should now be tracked correctly.  At SH auto-noexp is probably undesirable so you'd probably turn it off via 'xset noexp 0'.  This is now unnecessary – when you reach 200/201 noexp will be toggled off until you remort.  Your TNL set point remains unchanged and auto-noexp is technically still on, it is simply ignored while you are 200/SH.  You can still toggle noexp manually if you need to.
  
 - The window command buttons now 'light up' when clicked, which doesn't make anything happen faster, but I like how it looks.  The window plugin was always the last in line as far as getting updates because everything in it depended on the other two plugins, so its code will be getting a much-needed overhaul.
 
 - The GUI window also displays the cp level taken.  Red border means you can't take a cp at your current level, green border means you can.
 
It's a short list, but hopefully the differences are apparent.  If you encounter a problem, let me know.  Thanks for all of your support, reports, and advice that helped make the version 2 release successful in all respects!

# Search and Destroy v2.0 beta — 11 Aug 2018

- Beta revision 9 uploaded at 03:05 on 11 Aug 2018

Good morning ninjas and ninja fans, I have finally gotten around to merging the original three plugins (Mapper Extender, Search and Destroy, and Search and Destroy GUI) into a single plugin.  Version 2.0 should do everything that the originals did, while suffering none of the drawbacks.

As the beta release of version 2.0 there are no new features yet.  I expect this to have unresolved problems, but I've been doing campaigns with it over the last day and nothing's really caught fire.  Feel free to give it a try and let me know what you think!

Here is the outline of what's been done up to this point:

 - Removed the plugin-broadcast interface and its supporting code and replaced with conventional variable assignments and function calls.  Three separate plugins receiving mostly the same data made for a lot of redundant/triplicated code and CPU work.  All gone now.
 
 - Removed most of the redundant/duplicate code resulting from separate plugins having similar functions and utilities.  The    
   important ones are pretty much taken care of, but given time constraints and exhaustion from work I had to prioritize a bit
   and likely didn't get it all.  I'll clear up the rest in the next update.
   
 - Fixed duplicate alias/trigger names, of which there were a few.  Duplicate pattern matches should all be merged and the excess 
   removed.
   
 - The plugin help text is not working.  It took up a lot of space and was making it harder to browse the file 
   so I cut it out and put it in a text file for later.  Also removed the help button from the window because it 
   wasn't really useful.  I'd like to redesign the window layout and features but am not sure what to do yet.
   
 - Rearranged the XML code for aliases and triggers to be more compact, reducing file length by some 150 lines.  
   It makes it a lot easier to find and fix things.
 
 - Default start rooms for Ooku and Arboretum have been added.
 
 - I reworked init_plugin and there shouldn't be any problems at the login screen or login process.  Let me know if there are.
 
 - Since version 2 is an entirely new plugin, it has a different plugin ID which means that user-set area start rooms and 
   similar saved things will not carry over.  It's not feasible to try combining three sets of saved settings and ensure there 
   are no problems.  The new version is basically incompatible with the old.  I regret any inconvenience arising from this.
   
That's pretty much it for now.  Please let me know when things break so I can get them handled, and keep in mind that this is indeed a beta version which might crash or glitch on you.  General comments, suggestions, and questions are also welcome, as always.  The beta will run for a couple of weeks to a month, depending on feedback and further testing.  Good luck, and thanks for all of your support and encouragement!

# Search and Destroy 1.3.5 - 7 April 2018
Happy new year, ninjas and other fans of mine!  I'm happy to report that 1.3.5 is a really nice update.  Without further ado, here's what's new:

 - The process for getting cp target data has been redesigned.  The cp type check is the primary
    director of process flow and occurs after cp check, rather than during.  The number of required
    mapper DB operations is reduced by roughly half and all of the post-process filtering has been
    eliminated, further improving performance and reducing ambiguity.  This should finally put an
    end to most of the display and link-related problems that have plagued S&D since the beginning.
    
    As of April 27 the recent crashes and a few other issues discovered during the investigation
    should be fixed.  I guess we'll find out.  Let me know if not.
  
  Additional process improvements, bug fixes, and other changes include:
 
 - Unknown target links were glitchier than expected but Mapper Extender and GUI should now handle them correctly.
 
 - Adjusted the room cp filtering parameters to deal with high-level mobs in low level areas.  For
    example, living wall in Descent to Hell would come up as unknown because it's a level 85 mob in
    a level 35 to 55 zone.  Most of these should now be handled correctly.  A side effect of this
    change is that you'll probably see more 'redundant' room cp links than before.  Unfortunately,
    using the area level ranges for filtering is sub-optimal and given the number of exceptions and
    overly broad (or just flat out wrong) level ranges, the only good way to filter would be to
    store data for every mob, but at that point you're looking at something way more involved.
	
 - Cp type check moved to Search and Destroy, using cp info to get the data.  This removes the 
    escalating probability of mis-identification, which can happen if cp check is used instead.
	The cp level taken is also recorded at this time.
   
 - Room names containing parentheses are now matched correctly.
  
 - Mapper Extender should no longer crash due to missing area or mapper data (e.g. as happens when new areas
    are added to the game).
 
 - The area indexing process is only allowed run when your character state is 3 (standing), 8 (fighting), 9 (asleep), or 11 (sitting or resting).  This solves any issues related to the process running at inappropriate times, e.g. while logging in, afk, or writing a note.

 - Cp check output for room cp's is now easier to read.
  
 - Dead targets on room cp's now display correctly.

 - Xcp with no argument would always target the first mob in the list, even if dead, which could
    prove unhelpful.  Xcp now targets the first mob that is alive.
    
 - Xcp also skips over targets whose locations are unknown.
	
 - Xcp can now be set to automatically hunt trick, quick where, or do nothing after running to
    the target area (on area cp's).  The syntax is 'xcp mode [ht|qw|off]'.  The default has always
    been hunt trick, but sometimes that's not ideal and this allows some flexibility.  Has no 
	effect on room cp's since they directly state the room name.

 - Improved quest handling.  S&D has always worked with quests, but 'xcp' would overwrite the quest
    info and cause it to be lost.  The command 'xq' has been added which re-targets your quest mob.
 
 - Auto noexp has been updated to use GMCP config, making it about as reliable as it can get.
  
 - Removed a lot of dead, orphaned, or otherwise obsolete code and triggers; improved regexp for
    various triggers, etc.; and other general cleanup.

# Search and Destroy 1.3.4 - 9 December 2017
Happy birthday, ninjas everywhere.  We have a new update, which is more of a bug fix update than a feature update.  But 
there are some new things, and hopefully some of the glitchiness in 1.3.3 has gone away and not been replaced.

Search and Destroy:
 - Settings like noexp, etc. will be saved between sessions/installations.

 - New feature: xwhere.  It lets you 'where' multiple mobs quickly, which can be useful
   in many different situations.  'xwhere 10 mob' does 'where' starting at 1.mob and
   counting to 10.  'xwhere 10 20 mob' does 'where' starting at 10 and counting to 20.
   Previously I would do this using a command-line "for" loop, but got tired of typing
   them out and just wrote it into an actual command.

Mapper Extender:
- "xrunto" only works with the area keyword.  It no longer tries to match the area long
   name, or to guess the start room.  It still does partial matches on the area keyword.
   If no match is found, it will pull up 'area keywords <your text>' and display any
   matches.

   The problem is that the area keywords and long names have too many words in common
   and with partial matches it gets even worse.  This is why 'xrt desert' or whatever
   would sometimes go to the wrong area.  The "runto roulette" / go to random room in
   area problem can range from annoying to deadly.  I don't have a better answer yet,
   but for now, limiting input to areaid/keyword eliminates the errors and gives
   consistent performance.
 
- Added default start rooms for open clan halls, manor areas, and some other areas.

- Room cp links to non-questable (clan, manor, etc.) areas are no longer displayed.

- Room links are now filtered according to the level the cp was taken, rather than the
   current player level.

- Fixed a bug which spammed GMCP requests and broke target detection upon plugin install.

- Fixed a bug where 'xcp' sometimes sends you to the wrong target while on a room cp.

Mapper Extender GUI:
- 'xset' and 'xgui' are equivalent for window settings and commands.

- Font size and line spacing are saved between sessions/installations.

- Much-improved window resizing and performance.  Special thanks to Ylar for this!
   It's a bit glitchy, probably because fiddled with the code to address some minor
   details, but most of the time it isn't apparent.  To resize the window, use the
   widgit thing in the lower right corner, as with the standard Aardmush plugins.

- Re-added maximize and minimize window functions as right-click menu options.

Once again, thanks to everyone who has given me your support in this project, I've
learned a lot in working on it and I hope you all enjoy the results.  Thanks for all
the ideas, contributions, and technical advice.

To those who haven't supported me (of which there are a few people) your criticism
is valuable because it keeps me evaluating, and helps me moderate my enthusiasm so
that I don't lose perspective or get too carried away.  Thanks for that.

Happy searching and destroying, ninjas of aard.


# Search and Destroy 1.3.3 - 22 October 2017
Good morning ninjas, we have a new update today.  As usual, if there are any problems, let me know and I'll do
what I can.  Here we go:

- The campaign type detect should correctly identify the cp type when a room and the area 
  it's in have the same name.

- The display glitch where targets don't show up should be fixed.  Let me know if not.

- The current 'xcp' target is now highlighted in the GUI window.

- Room cp targets are now sorted by area.  Special thanks to Fiendish for helping me with this.

- The font size and line spacing can now be changed in the GUI window.  The commands are 'xgui fontsize \<number>'
  and 'xgui linespace \<number>'.  Defaults are 8 and 15, respectively.

- The cp list font will change between Lucida Sans Unicode and Segoe depending on cp type.  Segoe is a bit
  narrower than Lucida and it might allow more room cp text to fit in the window.  Xgui fontsize works on
  both.  

- "nx" and "nx-" now do 'quick scan' after the run.

- Removed all but the "?" button from the window title bar.  I never used them, did anyone else?

- Added "send to front/back" to the window title bar as a right-click menu.  The title bar buttons (including
  'bring to front') usually got covered up when sending the window to back, making them un-clickable.  Not helpful.
  As long as you can right click the title bar, it's easy to bring the window to front again.

- Finally removed the 'reset gui' commands and related code.  Their only purpose was to bring the window back after it glitched out and left the screen, but since that bug no longer exists there is nothing to reset anymore.

- Removed much of the spam that happens on Mapper Extender install, and when you take a new cp.  Also removed some
  old debugging output as well as "cp ch" and other echoes when the plugin sends commands to the mud.  The output
  looks and feels a lot cleaner now.

- Continued the trend of more code clean-up, regexp simplification, neater output appearance, and all that.

That's all for now.  Happy searching and destroying, and thanks for all your support!


# Search and Destroy 1.3.2 - 22 September 2017
- Added 'xcp' as an alias for 'xcp 1'.

- 'xcp' will retry if it fails because of "no object or data busy".  

- If you hit 'nx' too many times, you can go back by using 'nx-' or right-clicking
  the 'nx' button.

- Enlarged GUI buttons to make them easier to click.

- S&D now detects which type of CP is active.

- Target list is now filtered according to cp type.  This removes most of the extra 
list items displayed (mostly in area cp's) when a target location is both a valid 
area and room name.  Room cp's can still generate multiple links per target (as they
should) if the same room name exists in different areas.

- Simplified 'xcp' and 'cp check' syntax in Mapper Extender.  I get what WinkleWinkle
was doing with these crazy regexp's, but most wind up being complexity for their 
own sake.  Fiendish certainly doesn't use them in his scripts, and I can see why.
Unless anyone actually requires the complex versions, I'm looking at gutting the 
command interface and making it simpler and more consistent.

- Removed a lot of spammy text output (old debugging messages, etc.) plus other 
general cleaning-up. 

Lastly, on short notice, I'm implementing a change to correct a glaring omission that was brought
to my attention.  A few other things I was working on also made it in.  Hopefully they
aren't horribly broken:

- Hunt trick should now work for Navigators hunting through portals.  Previously, 
it would break because the portal hunt message didn't match the regexp.  It looks
functional to me now, but I'm not a navigator so please let me know if and when this
breaks.  If it works, it should remove the need to patch it yourself.  

- Navigator auto-hunt will be trickier.  For now, when you try to hunt through a portal, you
will be prompted to enter the portal and then autohunt again.

- The autohunt command interface has been redone, in line with the general simplification
plan mentioned above.  If anything goes wrong with it, let me know.  This wasn't rushed,
exactly, it just hasn't had as long to be tested as other things, but I fixed all of the
issues that I was able to identify.  Type "search help" to see the new command syntax.

# Search and Destroy 1.3.1 - 14 June 2017
Bug fixes:
- hunt trick will now correctly terminate after trying to hunt something that doesn't exist.
- hunt trick will now correctly terminate if you try to do it while resting, sitting, or sleeping.
- hunt trick and quick-where will no longer use 1.mob for its first
try.  It will just do 'hunt mob' or 'where mob'.  I don't think it matters which is used,
it seems to target the same thing either way, I just didn't like 1.mob.  If problems with
it let me know and I can change it back.
- campaign target window will now populate when taking a CP from a questor.  Before, it would
only populate when requesting from Commander Barcett.
- the problem with 'xrunto' sometimes taking you to a random-ish room is mostly fixed. If 
xrunto takes you to the wrong area, e.g. Fantasy Fields instead of 'fields' (Killing Fields)
go to (in this case) Killing Fields and 'xset mark' the start room again and that should fix it.

New feature:
- Auto-noexp!  When you're at low TNL and you can take a campaign at your current level, 
 it will turn on noexp and prevent you from over-levelling and missing a campaign.

   When plugin is installed, it defaults to off.  To turn it on, do 'xset noexp (amount)'.
 If you're on a CP but can take a new one at your current level, noexp will kick on 
 when your TNL drops below the given amount.  Noexp will kick back off after you finish
 your current CP and then go and take another one.  You can also toggle noexp off 
 manually via 'noexp' as usual.  For low levels I suggest setting it at 1000 TNL or so,
 and around 500 when you get higher and mobs award less XP.  You may need to go higher
 if there's a lot of double stacking with your daily blessing bonus.
 
# Search and Destroy 1.3.0 - 31 May 2017
- Search and Destroy is once again being actively worked on, and this time I'm in charge!
Good times are ahead!
- The bug causing the GUI window to 'jump' and leave the screen when you try to move it has
been fixed.  It is no longer possible for the window to get lost, stuck, or otherwise go
beyond the edges of the screen.
