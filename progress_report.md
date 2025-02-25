### February 11, 2025

Opened Repo & set up .md files 
Have already downloaded and confirmed the content of CR campaign 2 (141 episodes)files
Contacted CR by email form on their site to request permission to use their data with explanation of the project
Writing up rough draft project plan with some additional ideas in more detail

#### Next goals
- CR data included .py file to convert html text files to json files, run this -> OK
- Confirm with Stuart at Kryogenix origins of transcripts ->
	- CRTranscript (a fan movement) did most of C2 but according to CR [here](https://critrole.com/cr-transcript-closed-captions-update/) this changed around episode 54
- start building df for CR data to explore what is included (time stamps?) -> OK
- explore possibility of comparing with other similar data -> OK
	- Could not find transcripts for 4sd (the post-episode weekly recap/chat show)
	- Considering comparing with similar D&D liveplay podcasts with different casts & DMs 
		- CR data includes EXU DMd by Aabria (8 episodes) and Calamity DMd by Brennan (4 episodes) but there's a huge discrepancy in data volume
		- Dimension20 (another liveplay podcast) has fanmade transcripts [here](https://dimension20.fandom.com/wiki/Episode_Transcripts)
			- There are a couple D20 stories also DMd by Aabria if we wanted to look at those as a woman DM compared to CR
	- If these aren't ideal I can look elsewhere for other data but are my initial thoughts
	
### February 15

Completed my full Critical Role DF into its base level format
Sourced D20 transcripts for all seasons run by Aabria (+EXU, CR season run by Aabria)
- this will result in 45 episodes of a woman-run liveplay show (compared to CRs 141)
- thinking about adding in transcripts for the more casual chat/episode recap post-show for Aabria's seasons too (would make the total 82)

Contacted the teams who make the D20 transcripts. Have licensing info for them.
- Free to use, but asked them about downloads since site has no API info

Contacted Stuart about the origins of transcripts & am waiting for answers

### Next goals
- build dfs for Aabria data
	- D20 data does not include timestamp information and CR does, hoping this doesn't pose a problem or i can fix it
- pickle the CR data in its completed base format -> OK
- save D20 data one way or the other, start procesing
- read Jack's shared paper they helpfully shared with me
- ID helpful resources and get reading
- start some early data processing for CR data
	- adding colums for tokens, types, count, etc
	- some basic EDA to start 

### February 23
Identified method of downloading D20 transcripts, may not need webscraping after all, have to verify what they actually look like first
Got started on CR EDA - editing timestamp columns, getting to work on seeking out lines to eliminate (non-speech lines like "(laughs)") 
	- what to do with lines that are a combo of "(noise) and regular speech" - tagging vs eliminating -> OK

- Confirm with Stuart at Kryogenix origins of transcripts
- identify some known cases of speech overlap (I remember an event in episode 2 where two people yelled at the same time at someone else) to verify timestamp details
- I recall seeing some marker for singing in the text files but since singing is still a speech event I won't exclude it

### First progress report - Feb 25 2025
Critical Role data in good shape, ready to get working on. Confirmed what to do with all instances of (noise) and am working on creating split columns of "utterance" and 
"speech" so that only true speech will be tokenized and analyzed. My goal for this week is to add columns for: tokens, types, counts, sent lengths (to start) and
subcategorize by name into several categories, man, woman, DM, player, I may include two categories for man (with and without DM) since Matt talks *significantly* more
than everyone else. 
- Another sub-goal.... Ashley has the fewest lines by quite a lot too. I remember she was away quite a while to film for a few TV shows, I want to get some kind of 
attendance count for the episodes. Laura and Travis were also away on parental leave for a good while. This would be good information to have on hand when considering
% of totals

CR data processing steps (simplified) *[source](https://critrole.com/cr-transcript-closed-captions-update/)*
- CR html files came included with a python script to convert to json files created by Kryogenix (Stuart)
	- ran this, split into sep seasons, only read in from season 2
- Unpacking and normalizing CR data into desired df format (in cr_data notebook in data_samples) -> pickling in this state
- unpickle for more edits - fixing timestamps columns, splitting speech and non-speech utterances (cr_eda notebook in data_samples)
	- then moving onto what I described above
	- basic stats (up to this point) can be found in cd_eda
- I've also included one json file from the CR data in data_samples but will remove if it's determined I should

Dimension 20 (Aabria) data has been secured in .dox format. Next step is to convert it into a form I can use, read it into a notebook, and begin processing into a similar df format
- D20 data has no timestamp information which may affect overlap information (if I choose to include it ultimately)
	- transcribers said interruptions may be noted in text but I have to explore to confirm this still

Since Aabria isn't a permanent DM with Dimension 20, she tends to guest on several podcasts. One of these was actually on the Critical Role show,
at this time I've processed that data in the same format as the CR data above. I'll be doing my best to format the D20 data to fit in with that. 
I didn't include this notebook because it's identical to cr_data only with different files.

Though it's not in its final form at the moment I've included one episode of one of Aabria's seasons in its .docx forms in the data_samples files. 
They play as stoats in that one! 

D20 processing steps (simplified) *[source](https://dimension20.fandom.com/wiki/Episode_Transcripts)*
- convert into txt (or other) format from .docx
- organize and read in format and wrangle into a usable df all concatenated (multiple shorter seasons rather than one long one)
- Otherwise I plan to replicate the processing as closely as possible to the processing for the CR data.

Sharing plan:
- Still waiting for confirmation about CR data license info & how much/what I can and will share. Operating now on the assumption that I won't be sharing more than word types list
- D20 license info states the data can be shared and that any derivatives from it must also be made sharable under the same license
