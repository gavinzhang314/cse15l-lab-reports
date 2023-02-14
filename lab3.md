# Lab Report 3: Researching Commands

The command I will be researching is `grep`. The only source I used to understand these options is the manual shown by the `man grep` command on my MacBook.

## `-r`: Recursive Searching

The `-r` (also `-R`) flag tells `grep` to recursively search for matches with the given regular expression in all of the files in a given directory and its subdirectories. Therefore, while `grep` usually only accepts a file or list of files as its arguments, `grep -r` accepts directories in addition to files. This is useful for searching entire directories without knowing the structure of the directory and its subdirectories. For instance, if we wanted to search all files within `written_2/` for the word "Maxwell" without `-r`, we'd have to know that all of the files are either 2 or 3 levels deeper (depending on if they are in `nonfiction/` or `travel_guides/`) and then type `grep "Maxwell" written_2/*/*/* written_2/*/*/*/*`. However, with `-r`, we can simply do the following:

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

## `-l`: Output Filepaths Only

The `-l` flag tells `grep` to only output the filepaths of the files that contain a match, instead of also outputting the lines with matches as it does normally. This is useful for providing a cleaner output if all we care about is that a file merely contains a match. For instance, to find the files in `written_2/travel_guides/` containing the word `Bahamas`, we could do `grep "Bahamas" written_2/travel_guides/*/*`. However, the output is hard to sift through because many of the files that contain the word "Bahamas" show up multiple times. Instead, we can use `-l` to ensure that only the filepaths are listed:

```
$ grep -l "Bahamas" written_2/travel_guides/*/*
written_2/travel_guides/berlitz1/WhatToFWI.txt
written_2/travel_guides/berlitz2/Bahamas-History.txt
written_2/travel_guides/berlitz2/Bahamas-Intro.txt
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt
written_2/travel_guides/berlitz2/Canada-WhereToGo.txt
```

This also makes it possible to run `wc` on the output to count the number of files with a match. If we wanted to find the number of files in `written_2/` containing the word "museum", for instance, we can redirect the output to a file and then run `wc` on it:

```
$ grep -l -r "museum" written_2/ > matches.txt
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

## `-n`: Line Numbers
The `-n` or `--line-number` flag tells `grep` to also output the line number of each match. This is useful if we're interested in just one section of a file containing a long passage of text. For instance, let's say we were interested in learning about the United States' influence on the history of Cuba. To help us in our search, we could run the following command:

```
$ grep -n "United States" written_2/travel_guides/berlitz2/Cuba-History.txt 
15:In 1895 José Martí, Cuba’s most venerated patriot (who now has a street, square, or building named after him in every town), led the next and most important uprising against Spain. Born in 1853 and exiled at 18 for his political views, Martí became a journalist and poet. From exile in the United States he argued for Cuban independence. Martí was killed in an ambush during the War of Independence, which began in 1895 and in which some 300,000 Cubans died.
16:Throughout the 19th century, the United States, keenly interested in the island’s strategic significance and its sugar market, had become increasingly involved in Cuban affairs. A US purchase of the island from Spain had long been on the agenda, even though Martí had warned of becoming a satellite of the United States (“I know the Monster, because I have lived in its lair,” he wrote).
17:In February 1898 the U.S.S. Maine was sunk in Havana’s harbor, killing all 260 crew members. Although Spanish responsibility was never incontrovertibly established, the United States used the sinking as a pretext to declare war. US victory came swiftly, with Spain surrendering claim to the island by the end of the same year. A provisional military government lasted to 1902, when Cuba became an independent republic.
19:For the next five decades the United States, the largest importer of Cuban sugar, dominated the island’s economy and largely controlled its political processes. The period was rife with political corruption, violence, and terrorism. After 1933 Fulgencio Batista, though only a sergeant, orchestrated the strings of power through a series of puppet presidents before winning the presidency outright in 1940. He retired in 1944 but returned by staging a military coup in 1952. His venal dictatorship made it possible for him to invest some $300 million abroad by 1959.
20:Since the 1920s disillusionment with the nascent republic — with its clear dependence on the United States and its lack of political probity or social equality — had grown steadily. Although Cuba had the second-highest per capita income in Latin America, prosperity did not filter down from the upper classes. In fact, the World Bank in 1950 declared as many as 60 percent of Cubans undernourished. In Havana there was a greater concentration of millionaires than anywhere else in Central or South America, and the capital was dubbed “an offshore Las Vegas” for its brothels, casinos, and gangsters.
```

This tells us that we should read through lines 15, 16, 17, 19, and 20 to find the information we're looking for.

Similarly, if we wanted to learn about poet W. B. Yeats' relationship with Dublin, we can run the following command:

```
$ grep -n "Yeats" written_2/travel_guides/berlitz1/*Dublin.txt
written_2/travel_guides/berlitz1/HistoryDublin.txt:199:        galvanized the Irish — and in the words of Yeats’s poem, “All changed,
written_2/travel_guides/berlitz1/IntroDublin.txt:59:        to have produced three Nobel Prize winners for literature — Yeats,
written_2/travel_guides/berlitz1/WhereToDublin.txt:658:        the Abbey Theatre (see page 88). Founded in 1904 by W.B. Yeats, Lady
written_2/travel_guides/berlitz1/WhereToDublin.txt:846:        post-impressionist paintings of Jack B. Yeats (brother of the famous
written_2/travel_guides/berlitz1/WhereToDublin.txt:922:        roomful of Jack Yeats’s paintings. There are also watercolors,
```

This tells us not only what files we should look at but also where exactly we should look in them, saving us from having to spend time going through the entirety of all three files.
