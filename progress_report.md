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
	- what to do with lines that are a combo of "(noise) and regular speech" - tagging vs eliminating 

- Confirm with Stuart at Kryogenix origins of transcripts
- identify some known cases of speech overlap (I remember an event in episode 2 where two people yelled at the same time at someone else) to verify timestamp details
- I recall seeing some marker for singing in the text files but since singing is still a speech event I won't exclude it
