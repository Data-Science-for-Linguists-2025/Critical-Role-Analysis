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
- save D20 data one way or the other, start procesing -> OK
- read Jack's shared paper they helpfully shared with me ->
- ID helpful resources and get reading ->
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


### March 5

I've finally gotten my CR data into a DF that is ready for analysis. After a full weekend of regex I've split the dialogue column into three parts: 
dialogue, \[inaudible\] and \(sounds\) I've pickled it and I'm going to export it as a CSV to upload to my github in its completed form.

I have the D20 data to a point where I can start working. Rather than use the .docx format I saved the files in an html format and converted them to .json files.
These can be easily read into a df and treated with regex to split into two columns as the base format is one full column including name and speech together. 

Some new data pitfalls have arrived
- D20 transcripts are fanmade and therefore, some of the more recent episodes aren't finalized yet. They have full dialogue transcribe but not the associated speaker
	- I'm going to make note of which ones I'm missing and will check again at a later date, hoping more will be finished. 
	- for the time being I'll start processing the data into a good df & get the process down, if more episode finish i'll have the process saved
- D20 transcripts differentiate between when a person is speaking as themselves and when they're speaking in character
	- Ex. If player Brennan is speaking to the table in general it will be marked Brennan: but if he is speaking as his character it will be marked Tula:
	- Plan is to make a series of series similar to the CR data nonspeech work to make a "player" column rather than just names.
	Since each play has one character name it won't be difficult, any character name that isn't associated with one of the players will be the DM (Aabria)
	
Identified some early sources for research about hedging
	
Next goals:
- -> email Stuart finally -> OK
- -> read Jack's paper
- -> ID more source papers
- Save and upload CR DF as csv file  -> OK
- Get to processing D20 data into DF for study
- Make note of which episodes were not completed for D20 to check again in a few weeks -> MisMag2 ep 3-11, MisMag2 1-11, Burrow's End AP 6-10
- Fix the data files according to feedback so CR repository is as it should be


### Second Progress Report - March 21 2025

First, an update from Progress Report #1 feedback:
- I removed my notebook files from data_samples and created instead the [data_processing](https://github.com/Data-Science-for-Linguists-2025/Critical-Role-Analysis/tree/main/data_processing) folder
	- these files show the work I've done to my raw data to get it into a usable DF format. Lots and lots of regex.
- The [data_samples](https://github.com/Data-Science-for-Linguists-2025/Critical-Role-Analysis/tree/main/data_samples) folder now contains one episode from my CR data and one episode of my D20 data in its raw format and in an exported CSV file
	- Running the math, uploading the .json and .csv files of one CR episode is .006$ of the 147 episodes for campaign 2
- I've updated my README file to include column name descriptions, and will continue to update it for D20

LICENSE INFO:
License information has been secured for D20 data for a while now, for Critical Role, still in the air. 
I confirmed the source of the data from Stuart at Kryogenix, he got them straight off of the full length youtube videos. That means they're
primarily from a fan-created effort to subtitle the show, and half from the professional service CR hired part way through the season.
Very likely to play it safe I will keep my full data sharing to exclude full word tokens for the entire CR series, but I still hope to still 
hear back from the fan-transcribers with licensing information. For now, I'll be operating under this basis.

DATA INFO:
Critical Role data is ready for analysis in its current form.
D20 data is 99% to ready for analysis. I'm uploading a csv file of one episode from my DF, but will replace it once I've reached completed processing.

I wish I had more new data and analysis to upload, but so many of my efforts until now were focused on wrangling my data. 
What I can say is that my two data sets are pretty different from one another. The D20 data is a *lot* smaller than the CR data. 
At 99,344  lines (for now), the D20 data is only 22% the total of CR (at 434,052) lines.
Matt, the CR DM has 111,729 spoken lines, and Aabria has 34,659. However, when considered *in proportion* to the rest of the data sets, I believe this will still be interesting.

JUPYTER NOTEBOOKS:
I've updated my data processing files to include more informative section headers and included more notes and descriptions of the
step-by-step processes taken in the building of my dataframes. 

I plan to use the NEW CONTINUING method to my notebooks, and will update them accordingly as well with this information, and which step
of the project each notebook is associated with. The basic structure thus far is:
- processing and opening data (called file_data)
	- in this notebook I load in my data and get it into a basic dataframe format
- cleaning and organizing data (called file_cleaning)
	- this includes splitting nonspeech information from speech, correcting errors, (for d20) creating name columns etc

The third tier of continuing notebooks will be file_split, in which I work with the data in its split (final) format. 
This is where I will do analysis, splitting by role (DM vs Player), gender, and so on. I have taken very early steps into this work, but
not yet very in depth. When not working on homework three recently, I've been working on the regex to get my D20 data into a good format.
Now that it's almost complete, I can really dive in and get to work. 

DATA SHARING:
As I said above, I plan to not share the Critical Role raw data, but once I've done some processing, I will publish a completed .csv of my
CR data *excluding* "text" or any kind of word token columns. I will eliminate down to word counts and information derived from the text (speech).

I will, however, share a full csv of my D20 data. Per the license information, the transcripts are free to use for any purpose including commercial,
and I believe work done with the transcripts should be shared as well. If others want to use it, they should be free to do so.

LICENSE:
I will update my license.md to fit with *my* license information while noting the licenses my datasets are under elsewhere. 
Looking at the "choosealicense" quick guide I intend to post my data and information with the CC-BY-SA license type
(the same time I was able to get the d20 data under). Since my data comes from a community made with fan-lead efforts with the intention
to be shared with others, I want what I create from that to be shared under the same principle. 


### Third Progress Report - April 7 2025

Both data sets are in full working order. In my early analysis attempts I identified a few token lines that were problematic and were eliminated.
One was some encoding mistakenly transcribed and another was a produced song (not a song being sung live) for example.

From last time, some additional data was added. The question of jargon came up in discussions about what is worth analyzing in the data.
Notebook [here](https://github.com/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/DND_Jargon.ipynb)
My goal and process for measuring jargon in my speech data is this:
1. process and tokenize all text from the Player's Handbook, essentially the instructional book of how to play DND
2. conduct readability score testing on the full text to find a baseline of complexity for the text (to compare to later)
3. lowercase and create a set of the full PHB text
4. compare lists of PHB set and Norvig Google data set and return tokens not found in Google list -> this is the list of jargon

Began data processing [here](https://github.com/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/cr_analysis.ipynb) 
I've been using the new continuing method and numbering/describing the order of files in data_processing, but I intend the notebooks subfolder to hold
my JPN processing files in their final form to be read in. Let me know if I need to update this as well to make it obvious.

So far I've run the CR data through the basics, line count, tokens, word count, word length, types & type count, sent count, sent length, all with some
interesting visualizations and early analysis. 
Next steps:
1. Split the data into my pre-determined categories (men/women, player/dm)
2. look at these parameters by group instead of per player
3. Look into interruptions, hedging, and jargon by group
4. do readability score for groups too, just see if it's interesting
5. do all of that exactly again for the D20 data

My data files are complete, but not in the format I intend to share them in yet. I will be uploading what I can as soon as I can

Still need to update my license file for my data - I intend to share all that I can so that other people can use it if they choose to.
will update my README file with a link to my guestbook and wait for more thorough structure guidance to update anything else

Sorry for the late turning in! I spent the weekend so excited about data analysis I forgot to even check for deadlines
