# Lab Report 3: Researching Commands

The command I will be researching is `grep`. The only source I used to understand these options is the manual shown by the `man grep` command on my MacBook.

## `-r`: Recursive Searching

The `-r` (also `-R`) flag recursively searches for matches with the given regular expression in all of the files in a given directory and its subdirectories. Therefore, while `grep` usually only accepts a file or list of files as its arguments, `grep -r` accepts directories in addition to files. This is useful for searching entire directories without knowing the structure of the directory and its subdirectories. For instance, if we wanted to search all files within `written_2/` for the word "Maxwell" without `-r`, we'd have to know that all of the files are either 2 or 3 levels deeper (depending on if they are in `nonfiction/` or `travel_guides/`) and then type `grep "Maxwell" written_2/*/*/* written_2/*/*/*/*`. However, with `-r`, we can simply do the following:

```
$ grep -r "Maxwell" .
./written_2/non-fiction/OUP/Kauffman/ch1.txt:The considerations above led to the role of Maxwell’s demon, one of the major places in physics where matter, energy, work, and information come together. The central point of the demon is that by making measurements on a system, the information gained can be used to extract work. I made a new distinction between measurements the demon might make that reveal features of nonequilibrium systems that can be used to extract work, and measurements he might make of the nonequilibrium system that cannot be used to extract work. How does the demon know what features to measure? And, in turn, how does work actually come to be extracted by devices that measure and detect displacements from equilibrium from which work can, in principle, be obtained? An example of such a device is a windmill pivoting to face the wind, then extracting work by the wind turning its vanes. Other examples are the rhodopsin molecule of a bacterium responding to a photon of light or a chloroplast using the constrained release of the energy of light to construct high-energy sugar molecules. How do such devices come into existence in the unfolding universe and in our biosphere? How does the vast web of constraint construction and constrained energy release used to construct yet more constraints happen into existence in the biosphere? In the universe itself? The answers appear not to be present in contemporary physics, chemistry, or biology. But a coevolving biosphere accomplishes just this coconstruction of propagating organization.
./written_2/non-fiction/OUP/Kauffman/ch4.txt:My aim in the current chapter is to begin to investigate what we might mean, and hence see, by propagating organization. No easy journey, this. I will begin with Maxwell’s demon and why measurement of a system only pays in a nonequilibrium setting. In a nonequilibrium setting, the measurements can be stored and used to extract work from the measured system. Maxwell’s demon is the clearest place in physics where matter, energy, and information come together. Yet, we will find the demon and his eorts at measurement tantalizingly incomplete: You see, only some features of a nonequilibrium system, if measured, reveal displacements from equilibrium from which work can, in principle, be extracted. Other features, even if measured, are useless for detecting such energy sources from which work can be extracted. Thus, whatever the demon’s eorts, there remain the issues of just what features of a nonequilibrium system the demon must measure such that work can be extracted, how the demon knows to measure those features rather than other useless features, and how, once measured, couplings come into existence in the universe that actually extract work. Not good enough, I shall say, to assert that in principle, work can be extracted. How does work come to be extracted?
...
```

The `-r` flag tells `grep` to go through all of the subdirectories for us, meaning that we don't have to consider it.

Similarly, if we want to narrow down our search to one directory, we can just specify so in the paramater we pass to the command:

```
grep -r "Maxwell" written_2/travel_guides 
written_2/travel_guides/berlitz1/WhereToIndia.txt:        Himalayas. With British associate Maxwell Fry designing most of the
written_2/travel_guides/berlitz1/WhereToMalaysia.txt:        (Maxwell Hill), 12 km (71⁄2 miles) northeast from Taipin, was
written_2/travel_guides/berlitz2/Canada-WhereToGo.txt:New Brunswick’s capital is a pleasant, sleepy little town most notable for the splendid Beaverbrook Art Gallery. It was built by William Maxwell Aitken (1879–1964), who as Lord Beaverbrook became a great British press baron and a member of Winston Churchill’s war cabinet. (Although born in Ontario, he took his title from his home in Beaverbrook, New Brunswick.) Look for Graham Sutherland’s imposing portrait of the publisher of London’s Daily Express and other fiercely patriotic newspapers. But the gallery’s masterpiece is Salvador Dalí’s Santiago el Grande. Other important works include the English school of Reynolds, Turner, Gainsborough, and Romney, and Canadian paintings by Tom Thomson, Emily Carr, and Cornelius Krieghoff.
```

## `-m`: Maximum Matches
When `-m <number>` (or `--max=<number>`) is used, `grep` stops looking for matches in a file after the specified number of matches is found. This is useful for providing a cleaner output if all we care about is that a file merely contains a match. For instance, to find the files in `written_2/travel_guides/` containing the word `Bahamas`, we can do `grep "Bahamas" written_2/travel_guides/*/*`. However, the output is hard to sift through because many of the files that contain the word "Bahamas" show up multiple times. Instead, we can use `-m 1` to ensure that each file with a match is only listed once:

```
% grep -m 1 "Bahamas" written_2/travel_guides/*/*
written_2/travel_guides/berlitz1/WhatToFWI.txt:        waters off the Bahamas, Puerto Rico, and the Virgin Islands, but the
written_2/travel_guides/berlitz2/Bahamas-History.txt:Centuries before the arrival of Columbus, a peaceful Amerindian people who called themselves the Luccucairi had settled in the Bahamas. Originally from South America, they had traveled up through the Caribbean islands, surviving by cultivating modest crops and from what they caught from sea and shore. Nothing in the experience of these gentle people could have prepared them for the arrival of the Pinta, the Niña, and the Santa Maria at San Salvador on 12 October 1492. Columbus believed that he had reached the East Indies and mistakenly called these people Indians. We know them today as the Lucayans. Columbus claimed the island and others in the Bahamas for his royal Spanish patrons, but not finding the gold and other riches he was seeking, he stayed for only two weeks before sailing towards Cuba.
written_2/travel_guides/berlitz2/Bahamas-Intro.txt:The Bahamas and the Bahamians
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:Crafts. Bahamians have always had to fend for themselves, and this resourcefulness has led them to become proficient at a number of practical handicrafts, many of which make beautiful souvenirs. Straw goods are the most ubiquitous. The Seminole Indians of Red Bay on Andros are said to produce the finest work on the Bahamas, though each island has its own individual patterns and differences in style. It is still possible to watch the women at work on the islands of Andros and at George Town on Exuma. Straw work can be bought from small workshops in people’s homes or from the better quality straw vendors in Nassau. Prices can be high, but even small bowls make beautiful and practical reminders of your trip. The handmade pieces are likely to become rare within a couple of generations, because so few young Bahamian women are now taking up the craft. Be aware that much of the straw work, particularly the mass-market goods like hats and bags, is not made in the Bahamas but in Taiwan and China. If you want to be sure of getting genuine Bahamian straw work, buy from places such as The Plait Lady, who has a shop on Bay Street in Nassau; you’ll have to pay a little more but you’ll be sure you’re getting an authentic handmade work of art.
```

This also makes it possible to run `wc` on the output to count the number of files with a match. If we wanted to find the number of files in `written_2/` containing the word "museum", for instance, we can redirect the output to a file and then run `wc` on it:

```
$ grep -m 1 -r "museum" written_2/ > matches.txt
$ wc -l matches.txt                             
      91 matches.txt
```

## `-i`: Case Insensitive Matching
`-i` can be used to case-insensitive matching. This can be useful since it means that we can search for words what may be capitalized in titles and headers:

```
$ grep -i -r "readings" . 
./written_2/non-fiction/OUP/Fletcher/ch5.txt:Alternative Readings
...
```

Additionally, `-i` means that matches at the beginning of sentences will also be found:

```
$ grep -i -r "educational" .
...
./written_2/non-fiction/OUP/Berk/ch1.txt:Educational practice followed suit, moving back toward traditionalism. As Scholastic Aptitude Test (SAT) scores of American high school graduates plummeted and concern over the academic preparation of American children and youths became widespread, a “back to basics” movement arose that, by 1980, was in full swing. Academic preschools ﬂourished, and kindergarten and primary classrooms returned to whole-class, teacher-directed instruction relying heavily on workbooks and frequent grading, a style still prevalent today.43 

...
```
