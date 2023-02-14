This lab report will explore the different command line options for the bash command `grep`. `grep` (in the most basic terms) returns all lines in a file containing a phrase. For example, if I want to search written_2/travel_guides for "short holiday", I can use grep to discover Mallorca is the place to be.

<img width="769" alt="image" src="https://user-images.githubusercontent.com/122497388/218662897-c3aab578-ab6e-420b-81a3-98c0fde3477f.png">

# grep -i
To do a case-insensitive search, `grep -i "phrase" file` can be used.

<img width="792" alt="image" src="https://user-images.githubusercontent.com/122497388/218666363-e361872b-d998-4405-80c5-bdbe8d2769ee.png">

<img width="773" alt="image" src="https://user-images.githubusercontent.com/122497388/218665656-dfe0a973-8ad5-4bb5-af58-47fc6f5dcb33.png">

This allows a much more accurate search in the cases where a word could be capitalized at the beginning of a sentence perhaps.

# grep -R
`grep -R "phrase" ` can be used to search for a phrase in the working directory and all its subdirectories.

<img width="791" alt="image" src="https://user-images.githubusercontent.com/122497388/218667644-04ecf6ff-c73f-498d-a8d1-ade4e992f293.png">

<img width="794" alt="image" src="https://user-images.githubusercontent.com/122497388/218668270-0a26d584-041e-4275-a1ed-32ce389571ee.png">

This works well for an easy search without worrying about patterns and making sure all files of a certain type are located in a certain directory.

# grep -c
`grep -c "phrase" file` can be used to count the number of times a certain phrase appears in a document.

<img width="743" alt="image" src="https://user-images.githubusercontent.com/122497388/218668916-a5441301-72f7-4c9f-a83c-f971614e8f83.png">

<img width="711" alt="image" src="https://user-images.githubusercontent.com/122497388/218669416-655a4949-2ba3-4369-8010-1bf5f736c1b8.png">

This can be useful, especially if the phrase appears several times in a line.

# grep -w

`grep -w "phrase" file` can be used to search for an exactly matched phrase of full words. 

<img width="796" alt="image" src="https://user-images.githubusercontent.com/122497388/218671232-d9da5965-8376-4cae-a484-f3de23653738.png">

This is useful for a more specific search for an exact phrase, when you don't want to count other tenses or forms of the first and last words.
