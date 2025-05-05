Ashley Bakaitus
April 29, 2025

# Final Report

## History

It took me some time to find inspiration for a project subject. I'm glad I was inspired to look into something I personally really enjoy: D&D!<br>

Sourcing my data was not very difficult. Both shows have very dedicated fans who have put in a lot of work to transcribing, editing, and making the scripts available to the public for use.

Data cleaning was, by far, the part of this project with the most bumps in the road. Those notebooks can be viewed [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/tree/main/data_processing/).<br>
This was my first time working with json files, and the CR file was very nested. Once I studied up on json normalization, though, getting a base dataframe was just a matter of defining a few functions and testing them out!

For Critical Role, it was the ["nonspeech"](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/data_processing/2_cr_cleaning.ipynb#Splitting-and-cleaning) column that was the most time consuming.
I had several false starts working at it to separate out and get a clean column containing only speech information. One early attempt included cloning the speech column entirely with the thought of deleting anything in (brackets) from one and deleting anything not in (brackets) from the other. 
It wasn't quite as simple as that in the end, and I ultimately found the method of creating many small Pandas Series much more productive. I frequently ran into my regex scanning and separating capturing the same index rows multiple times, giving me a duplicate index error, but I fixed it by creating more and more narrow Series and tweaking my regex. 
It took a long while on my first go, but the feeling of when my duplicate index check first cleared with no duplicates was beautiful. 

With the Dimension 20 data there was much more cleanup required. The regex routine was less complicated since I'd spent so much time on it before, but the data was more difficult. Everything was included in the same column as the speech, and nonspeech information like sound effects was not marked with brackets. 
While this took more time, there were just a few more steps to undertake, seen [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/data_processing/2_aabria_cleaning.ipynb#Concatenating-and-Splitting).

## Data Information

I ended up with a total of 201 json files (147 CR and 54 D20) in the shape of two dataframes. Once all dataframes were in their final forms, this put us at 434,050 rows (or speech turns) in the Critical Role data, and 63,602 turns in the D20 data.

The Critical Role data is one full campaign, or adventure, played start to finish over a period of roughly four years. The group is made up of one DM and seven consistent players. There are a handful of guests who appear for an episode or two who are combined into an "other" category for tidiness sake in my analysis.<br>
The Dimension 20 data consists of four campaigns of varying lengths, and three seasons of their post-game chat show they do about the episode just played. 

Critical Role has four players who are men, three women, and a man as their DM.<br>
Dimension 20, in these sets, have eight players who are men, eight who are women, two who are nonbinary, and a woman as their DM.

## Motivations & Research Questions

My goal for my project is to conduct a discourse analysis on these two data sets to look into the balance of DM to player speech between a man DM (Critical Role, Matt) and a woman DM (Dimension 20, Aabria).<br>
A secondary goal, while looking at the data, was to consider the balance at a table between players themselves, without the DM. Are players who are men or women talking more often, saying more words, taking more time? Or is there more of an equal balance?

## Analysis

My individual analysis for the two data sets can both be explored in my [notebooks/](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/tree/main/notebooks/) folder in my project hub.<br>
The files cr_analysis.ipynb and d20_analysis.ipynb cover the numbers and my analysis and interpretations per set in some detail, and so this section will be dedicated to the *comparison* of the two.

I did several more steps on the Critical Role data since it's where I started, like word lengths and average sentence length for sentences over a certain length. However since they were not extremely informative I did not repeat them for D20 and won't be further analyzing them.<br>
Similarly, my early intention for this project was to include interruption as one of my metrics of study. I address this at the end of both notebooks, but wanted to touch on it here as well. Without a significant time commitment, this aspect was difficult to quantify and was not analyzed. 

### Speech Turns

**Critical Role**

![screenshot](figures/cr_SpeechTurnGender.png)


**D20**

![screenshot](figures/d20_SpeechTurnGender.png)

In consideration of players, both groups of men take more speech turns proportionally to anyone else, including the DM. I address the issue of attendance in both of my individual analysis notebooks [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/cr_analysis.ipynb#Exploring-Results) and [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/d20_analysis.ipynb#Exploring-Results).<br>

Men outnumber women in Critical Role and have the more consistent attendance records, and as a result it's difficult to state decisively that men take more turns at that specific table, but in this dataset, they do. <br>
Interestingly, even without the new inclusion of nonbinary players in Dimension 20 data, men take 14% more speech turns than women do. However, while there are eight participants per group, two of the men appear in multiple seasons being looked at in the data.<br>
This inclusion of two players more than once may be affecting the proportions quite a bit. There are three repeats among them, if the casts were different but they were still men, that would make the totals 11 men to 8 women instead.

What I'm most interested in, here, is the fact that when it comes to speech turns, the two DMs are not so widely different. Matt takes a little over a quarter of all speech turns, and Aabria a bit under a third of turns. <br>
With only a 5% difference between them, proportionally to their players, I'm fascinated that they've landed quite closely together. It would be difficult, of course, for a single DM to out-speak a group of 3+ people alone, but the amount they do have is no small feat. <br>
There are a total of 422,576 speech turn rows in the Critical Role data, meaning that over 100,000 belong to Matt alone. Similarly, D20 has 63,602 speech turn rows, with just over 21,000 belonging to Aabria.


### Word Count

**Critical Role**

![screenshot](figures/cr_TokCountGender.png)

**D20**

![screenshot](figures/d20_TokCountGender.png)

As above, I have gone over the separate findings for these charts in their respective notebooks, [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/cr_analysis.ipynb#Word-Count) and here. <br>

Because the total words count among players for Critical Role hover at about the same 60/40 split as the speech turns chart did (+1.8%), I feel like we are truly seeing the attendance issue at play here.<br>
When the men at Critical Role speak up, which is more often than the women do, they are not taking up an extraordinary amount of time proportionally. <br>

With Dimension 20, however, men are saying many more words than women or nonbinary players per speech turn. Their share of words compared to speech turns increases 9.5%!<br>
The men of D20 take a little more speech turns than other players, and they say a lot more words during those turns.

Again, the two DMs in regards to total word counts are not so different to each other in proportion to their players, only a 0.8% difference between them with Aabria in the lead.<br>
Critical Role has a total of 3,676,893 word tokens in all speech data, and D20 has 784,575. Despite this vast difference in total spoken words, I'm fascinated to see that there's a settling proportion for both DMs in a very very similar range.


### Sentence Length

**Critical Role**

![screenshot](figures/cr_SentLenGender.png)

**D20**

![screenshot](figures/d20_SentLenGender.png)

Unsurprisingly, both DMs lead the pack when it comes to average sentence length. Even though Aabria has one player with longer sentences than her, seen [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/d20_analysis.ipynb#Sentences-and-sentence-length), she still leads over the players when grouped by gender.

Something I found particularly interesting when comparing sentence length across both data sets is that Dimension 20, on average, has longer sentence lengths among all players. 
Women players in D20 have sentences 0.11 words longer than CR, men 1.28 words longer, and CR has no nonbinary data to compare to. 
When it comes to the DMs, though, Matt actually takes the lead by by .28 words per sentence longer on average.


### Hedging

For the hedging measurement (conducted [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/cr_analysis.ipynb#Hedging) and [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/d20_analysis.ipynb#Hedging)), I measured frequency per thousand spoken words. 

The results are below:

**Critical Role**

Women (3 people) have 4921 instances of hedging phrases<br>
Men (4 people) have 7769 instances<br>
The DM, Matt, has 3656 instances

For every thousand words spoken per group:<br>
5.68 words spoken by women,<br>
5.75 words spoken by men, and<br>
2.6 words spoken by the DM are among the scanned for hedging words and phrases.

**D20**

Women (8 people) have 899 instances of hedging phrases<br>
Men (8 people) have 1930 instances<br>
Nonbinary players (2 people) have 309 instances<br>
The DM, Aabria, has 722 instances

For every thousand words spoken per group:<br>
6.93 words spoken by women,<br>
6.25 words spoken by men,<br>
5.64 words spoken by nonbinary players, and<br>
2.34 words spoken by the DM are among the scanned for hedging words and phrases.

And to refresh the memory, Critical Role had over 3.6 million words, and Dimension 20 had around 784,000. 

I think that in this *type* of data in particular, hedging plays an interesting role. Rather than the typical understanding of hedging: a softening of language, a politeness marker, or a culturally gendered speech phenomenon.<br>
Hedging in the context of a D&D game plays a very different role. For one, uncertainty. Players don't know what the DM knows. They don't know the plot, the rooms they're in, who is waiting to ambush up ahead, nothing.<br>
It is their job, often with the collaboration (and ideally cooperation) of their dice, to uncover those facts through exploration. Because of this, they are often genuinely in the position of uncertainty, and hedging language may appear as a result.

On the other hand, DMs proportionally have quite a high amount of hedging! Looking at the pure counts, Matt alone has almost as many hedging instances a group of three people, and Aabria is the same but with a group of eight!<br>
For a singular person, this is quite a high appearance of hedging words and phrases. <br>
My interpretation of this is because, while the DM may know all of the information I listed above, they will very likely want to withhold it somewhat often. At least until a player is able to figure it out through investigative thinking and good dice rolls.


### Jargon

I wish I'd thought of jargon earlier on into my research and data treatment! I think it's such an exciting and interesting topic to study and to attempt to apply a measurement to.
Building a list of D&D jargon in my notebook [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/DND_Jargon.ipynb#The-Jargon-List) was a fun first step, and I'm interested in building a more accurate list with more time dedicated to it.

Measurements of jargon were conducted [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/cr_analysis.ipynb#Jargon) and [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/d20_analysis.ipynb#Jargon). 

For this one I measured per million spoken words.<br>
The results are below:

**Critical Role**

For every million words spoken by the members of the group in question:<br>
304.8 words spoken by the women players (3 people),<br>
285.2 words spoken by men players (4 people), and<br>
262.6 words spoken by the DM will be from this jargon list.

**D20**

For every million words spoken by the members of the group in question:<br>
154.26 words spoken by the women players (8 people),<br>
211.75 words spoken by men players (8 people),<br>
73.01 words spoken by nb players (2 people), and<br>
201.71 words spoken by the DM will be from this jargon list.

Similar to the hedging language above, both DMs in proportion to groups of players produce quite a lot of jargon! 

Now, these numbers of course come down to which words specifically made it into the list of jargon - words from the Player's Handbook that were not found in the Norvig Google Unigram data.<br>
A lot of those were spell types (like cantrip, a spell a magic user can cast at-will unlike other spells which are limited) and spell names (thunderwave, thaumaturgy, revivify, etc).<br>
Depending on what character type they're playing, these words will show up more or less frequently. If you aren't a magic user, these words won't appear. <br>
In the case of the DMs, as narrators of the full story, I find it natural that they have such a high concentration of jargon proportionally to the rest of the table. <br>
The DM narrates according to all of those players, any non-player character (NPC), the surroundings, the history of the world, and runs any combat encounters.

There is a pretty large drop off in jargon frequency from Critical Role to Dimension 20, not just between DMs but overall. <br>
In my opinion, based on my familiarity with both podcasts, genre comes into play at this question.

Critical Role campaign 2 is a more "traditional" D&D game, what someone who is maybe only familiar through modern media like Stranger Things would think of. <br>
Dragons, monsters, horses and wagons, a lot of medieval style imagery mixed with a sort of Lord of the Rings style high fantasy with elves and dwarves and a great evil at play.<br>
It just so happens, of course, that with this being tradition, that this is what is also talked about in the Player's Handbook, from which the jargon list was derived.
On the other hand, Dimension 20 has a variety of genre in this data, an adventure where the players are stoats on an adventure or modern teenagers being taken to a magical school for example. Not to mention the chat show which is of an entirely different genre and style altogether.


### Readability

Only considering the results from the improved second run of the readability score testing. Our baseline score as conducted on the Player's Handbook [here](https://nbviewer.org/github/Data-Science-for-Linguists-2025/Critical-Role-Analysis/blob/main/notebooks/ReadabilityRedux.ipynb), which has a pretty concentrated usage of D&D-focused vocabulary was 56. Ranked as "difficult to read" but on the easier side of it, around a 10th grade level. The spoken data scored much higher (and much easier) than the book, which makes sense. Almost all of the rankings were at a "conversational" level or easier. Since it *is* conversation, this feels like a reasonable assessment. 

What I found most interesting is that, while all players scored in the 90+ range of very easy to understand, both DMs were scored at a more difficult range than the players. I believe this goes hand-in-hand with the jargon score. We saw that DMs have a high rate of jargon in proportion to their players, and both DM word clouds were more densely populated than the players. Many of the "jargon" words in the Handbook that made it to the defined list were specialized and a bit long. More inclusion of jargon would likely correlate to a lower (more difficult) readability score. 
Both DMs are 87 and 89, with Aabria ranked just a little bit easier than Matt. 


## Conclusions & Reflections

Going into this project, I found myself thinking that if I found a significant difference or not in any of my measurements between a man DM and a woman DM, it would be an interesting result either way.

For the most part, in my interpretation, there is not a huge different between our DMs in regard to speech turns taken, total words spoken, or average sentence length. 
Aabria leads by a small margin in speech turn and word count, and Matt leads by little over one full word per sentence on average. 

In the future, or with more time on my side, I would like to run some statistical test to verify the significance (or lack of) these small differences. 
Without those tests, though, by appearance and by the proportion of the DMs data to the totals and in comparison to the groups of players, it appears that there is not too notable a difference between either DM.
To me, what I interpret this data to indicate is the following:

Both of the DMs being looked at here and studied, Matt from Critical Role and Aabria from Dimension 20, are professionals in the field. Both of them are trained in improv and acting, and both of them have years, decades of experience in the DMs seat behind them.
I think that rather than the data here showing that a woman DM or a man DM does one thing differently to one another, it's more the case that these two represent something of a "golden ratio" of how much a DM should be speaking in comparison to their players. 
Talking any less than is shown in this data risks players being uninformed, unguided, and becoming detached from the story (and not having all those speech turns and words to say!).
Talking too much more than the more than a quarter to less than a third range observed in particular in the would overpower the players, who need time time and space to interact with the story to help it to move forward.

In the question of gender at a D&D table, though, the player data is quite interesting in that sense.

In 1980, Dale Spender published her book "Man Made Language". In her book she investigated if the "talkativeness" ascribed to women in pop culture is actually observed in reality. 
Her findings showed that if you measure in amount of words or in minutes, men speak more in mixed-gender groups (Albright). I was unable to measure minutes spoken in these datasets, but it takes time to speak and we know men took more speech turns, said more words, and had longer sentences among players.

## Resources

“Episode Transcripts.” Dimension 20 Wiki, Fandom, Inc., 2022, dimension20.fandom.com/wiki/Episode_Transcripts. Accessed 29 Apr. 2025.

Flesch, R. (2016, July 12). Guide to Academic Writing Article - Management - University of Canterbury - New Zealand. Web.archive.org. https://web.archive.org/web/20160712094308/http://www.mang.canterbury.ac.nz/writing_guide/writing/flesch.shtml

ila. (2020, November 24). Speaking Up: The Double Bind of Women’s Voices in Business. The Startup. https://medium.com/swlh/speaking-up-the-double-bind-of-womens-voices-in-business-592b0b56732c

Langridge , Stuart . “Critical Role Linked Transcript Search.” Kryogenix.org, 2025, www.kryogenix.org/crsearch/.

Mearls, Mike, and Jeremy Crawford. Dungeons & Dragons Player’s Handbook. 5th ed., Renton, Wa, Wizards of the Coast, Aug. 2014.

Norvig, P. (2009). Natural Language Corpus Data: Beautiful Data. Norvig.com. https://norvig.com/ngrams/

Readable. (2023). Flesch Reading Ease and the Flesch Kincaid Grade Level. Readable. https://readable.com/readability/flesch-reading-ease-flesch-kincaid-grade-level/

Scott, B. (2023, August 14). The SMOG Readability Formula, a Simple Measure of Gobbledygook. ReadabilityFormulas.com. https://readabilityformulas.com/the-smog-readability-formula/

Spender, D. (1980). Man made language. Pandora.
