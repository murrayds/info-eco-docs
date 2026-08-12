---
title: Taking Notes
---

Effective note-taking is essential for making use of the vast and unweildy scientific literature, and for providing a resource for yourself. The core task of note-taking is syntehsis. Synthesis forces you to understand the article and why it is significant. It also offers the material benefit of making it easier to lookup and remember the article later, which can be essential when managing hundreds (or even thousands) of references. 


# Taking notes on an article

**Length:** Notes should ideally be short, around 1-3 paragraphs of actual content. Longer is justified for long texts (like books), or particularly important texts

**Metadata:** Some basic metadata makes indexing and retrieving notes useful in the future,
- A series of 2-5 tags that describe the main themes and topics of the paper. Tags are short, usually just one word. When coming up with tags, think about what we might use to search for the paper. There should be some consistency in tags, such that the same tag appears across multiple papers. Tags are usually prefixed by the "#" character. For example, "#MachineLearning", "#LLM", "#Evaluation". 
- A reference of the paper that could be copy/pasted into a reference manager. I usually use APA formatting for this. There exist many tools to build such references automatically (e.g., [this one](https://citation.crosscite.org/))
- A reference to the paper in bibtex, a machine-readable format is used with Latex writing software. Including this makes it easy to quickly drop references into a writing project. There also exist many tools to create such references automatically (e.g., [this one](https://www.doi2bib.org/bib/https://doi.org/10.1038/s41562-021-01220-7))

**Major sections:** Good notes will often have multiple small sections that describe key aspects of the paper.
- *Definitions of key terms:* if there is some important concept or term that is used in the paper, then offer a quick 1-2 sentence definition
- *Main takeaways*: Provide a summary of the paper in 1-2 sentences. This is especially helpful for helping to remember a paper. 
- *Methods*: Provide a very quick description of the methods and any notable choices made in the paper. This doesn't have to be in depth, just highlight main points paying particular attention to anything that seems unique compared to other studies
- *Significance for current project*: What is the overall significance of the paper *especially in regards to the current project*. This one is tricky, because ideally we want notes that can be useful across project. However, often our reading a paper is motivated by the current project. Providing 1 sentence summarizing *why the current paper is important and why we should reference it in our current paper* can be incredibly helpful. 
- *Key Quotes*: Often there are sentences in a paper that are particularly insightful or do a good job of summarizing its overall argument. It can often be a good idea to list a couple of these quotes. 

In my own note-taking I almost always include appropriate metadata, however my note-taking tends to be more informal and so I don't follow the major sections exactly, but the elements are still there in my summaries. Moreover, my approaches to note-taking drift over time; while the above procedure describes my current note-taking, it remains in flux as I continue to read and refine my approach. It is important to develop your own strategies by reading lots of lots of papers and finding strategies that work for you.

An example to follow might be McDiarmid et al., (2011), which is a paper I read recently and I think demonstrates the overall structure (though lacking explicit sections) of my note taking. 

## Example note for an article

> #### McDiarmid, A. D., Tullett, A. M., Whitt, C. M., Vazire, S., Smaldino, P. E., & Stephens, J. E. (2021). Psychologists update their beliefs about effect sizes after replication studies. In Nature Human Behaviour (Vol. 5, Issue 12, pp. 1663–1673). Springer Science and Business Media LLC. https://doi.org/10.1038/s41562-021-01220-7
>
> #article #replication #psychology #belief #consensus #selfcorrection 
>
> This paper argues that, if science is self correcting, then individual scientists should update their beliefs in light of new and conflicting evidence. The authors test this by exposing researchers in psychology (holding a graduate degree, many PhD students and postdocs) to original studies making strong claims of large effects, and then following up with exposure to the counter evidence from a large and rigorous replication study as part of the Many Labs project. In the experiment, participants (n=1,096) are explicitly asked to provide an estimate (prior) of their belief that the effect is non-trivial. After exposure to the replication, they are then asked to provide a new estimate. This design allows for quantitative estimate of belief change in light of counter evidence. The study also includes components to measure psychologists' degree of investment in the study (and so, motivated reasoning), intellectual humility, and so on. 
>
> The results demonstrate three broad conclusions:
> - Consistent with authors' predictions, psychologists *do in fact* update their beliefs > after exposure to the replication, though not to the extent as would an ideal Bayesian > agent update
> - Contrary to their predictions, the authors observe little evidence of motivated reasoning when psychologists evaluate counter-evidence resulting from a replication
> - Belief updating is associated with slightly higher intellectual humility (a six-item measure used in other studies), but it is not associated with personal investment in the findings (self reported) or expertise with bias (e.g., psychological domain knowledge of how beliefs are influenced by personal bias)
>
> One thing they close on is the visibility of replications,
> 
> > Our study design placed replication results front and centre in the attention of interested researchers. However, a persistent problem with replications is that they are rarely published, and, when published, are rarely linked to the original results being replicated. This severely diminishes the potency of their impact. Our results show that replication can work when researchers are made to see their results


# Taking notes on a book

Taking notes on a book can be challenging. For an article, it if often relatively straightforward to summarize its key arguments. Books however are larger, with greater complexity in argument and lines of evidence. Simply scaling up my approach for taking notes on a scientific article isn't likely to be effective. Instead I suggest taking a whole different approach.

The core idea is to approach note-taking as answering a series of guiding questions concerning key elements of the book and its argument. 

The first question is ***What are the key concepts of the book?*** By concepts, I mean theoretical constructs and other important ideas. For example, [[toyama_2015_geek|Toyama (2015)]] introduces the idea of the "*Law of Amplification*". Pulling these questions out is important as they are (a) often core to understanding the text, and (b) the most portable elements of the book, such that they can be most readily applied to different situations. 

The second question is ***What is the main argument of the text?*** This can be the most difficult to answer and not always obvious. However, authors usually write books to argue something or make some point, and teasing this out is essential to understanding the text and remembering the significance of the book when you return to your notes. Try to keep this to at most one paragraph. For example, consider the following for [[toyama_2015_geek|Toyama (2015)]]:

> This text argues *against* techno-utopianism or techno-optimism; this is the position that technology will primarily be a force that solves human problems. However, Toyama is not a techno-pessimist. Rather, he takes the position as social determinist, arguing that all problems are only ever human problems. Technology, Toyama argues, can only ever amplify existing human behaviors, whether good or bad, and does little to fundamentally change human behavior. 

The third question is ***What lines of evidence does the author use to support their argument?*** In general every book that makes an argument must try to supply evidence to back it up. This may be quantitative evidence, examples, historical case study or logic, and so on. They likely use a mixture of these pieces of evidence. If there are specific numbers, what kind? If particular case studies or examples, what are they? For example, in his book *Geek Heresey* (2015), Toyama draws on personal experience of his time deploying educational technologies in Ghana and other countries. In other parts of his book he relies instead on purely rhetoric, stating his values (informed by his experiences) and making conclusions from these assumed values. Sometimes the evidence and support is not obvious, or may not appear like evidence at first, but it is always present. 

The fourth question is ***What is the structure of the book?*** Roughly, how are the arguments and evidence in the book arranged? What is the general flow of the arguments through the text? Where does the author begin their argument, and where does it end? Documenting structure (a) makes it easier to understand the argument, and (b) creates a map for how to return to the book to find relevant portions of the argument later. 

The fifth question is ***What literatures does the book draw on?*** Most academic books draw on particular scientific communities. For example, Toyama (2015) pulls mostly from *Science & Technology Studies*, *Development Studies*, and *Information & Computing Technology for Development (ICT4D)*. When beginning a literature review, it can be challenging to know these communities, but it becomes apparent after some experience. 

The sixth question is ***Who is the intended audience?*** Authors always have an audience in mind when writing a book. Generally, this will be academics, but what disciplines? Other times they may be making points about policy or industry or some other stakeholder—who would these other stakeholders be?

In addition to these questions, it is also incredibly useful to mark down quotes and sections of the text that capture its critical significance. I find it best to select quotes that are at least several sentences in size, and which summarize major points or make interesting arguments. Also select quotes that you simply find interesting, regardless of their centrality to the books's argument. I suggest selecting at least 5 quotes. 

While many of my own notes have a *relevance to my research* section, I actually no longer believe that this is useful. Effective notes of the kind I outline here should be project-independent, so that they can remain useful even as your research evolves over time. I encourage taking advantage of other summarization formats, such as annotated bibliography, for project-specific notes. 

Note that this is an *ideal system*. This plan never survives contact with the paper (or screen). Often I fall short of taking appropriate notes (as can be seen from my posted examples) whether for laziness or because the text doesn't merit the effort. Other times the structure of the book doesn't lend itself to these questions, and may be better off with a different *ad hoc*  note-taking approach. This is fine! It is merely a simple baseline approach to making effective notes, and the rules can be broken whenever necessary or useful.

## Example note for a book

> Toyama, K. (2015). Geek Heresy: Rescuing Social Change from the Cult of Technology (F First Edition edition). New York: Public Affairs.
> #book #sts #technology

> ### Key Concepts
> 1. **Law of Amplification:** This is the idea, not coined by Toyama but developed and > extensively used, that technology serves as merely an amplifier of already-existing human behaviors. Technology amplifies both good and bad behaviors. A good teacher given a smart-board will put it to use. A bad student given a laptop will use it to play games. > This idea is used to reconcile the effect of technology from a social determinist perspective—technology is never the cause of behavior, just an amplifier.
> 2. **Packaged Interventions:** Toyama uses this idea to discuss ready-made solutions to problems that are advertised as able to make improvements when deployed to any context. For example, a "laptop for every kid" is a packaged intervention—it promises radical improvements with relatively little investmenet, promises to provide knowledge access and enlightment to all, and promises to do so anywhere. However, as Toyama shows, this intervention is often lacking—laptops are rarely an improvement to education, and only succeed when there are good teachers and resources to take advantage of them. In a sense, packaged interventions are any intervention that don't focus on addressing the human-causes of social issues. 
> 3. **Intrinsic Development:** Often referred to as the development "heart, mind, and will", which Toyama uses "intrinsic development" to refer to the virtues that should be cultivated in individuals. Heart refers to intention, i.e., does someone want to work for the benefit of others (good), or their own personal gain (bad); mind refers to discernment or ability to make use of knowledge, i.e., does someone follow sound medical advice on vaccinations (good), or follow poor advice about vaccines and autism (bad); will refers mostly to "grit", "follow-through", "perseverance", and other such ideas, i.e., will someone actually commit to an exercise regiment (good), or continue a sedentary lifestyle (bad). Toyama argues that international development should prioritize the intrinsic development of people, rather than on fixing external factors. 
> 
> ### What is the main argument of the text?
> This tech argues *against* techno-utopianism or techno-optimism; this is the position that technology will primarily be a force that solves human problems. However, Toyama is not a techno-pessimist. Rather, he takes the position as social determinist, arguing that all problems are only ever human problems. Technology, Toyama argues, can only ever amplify existing human behaviors, whether good or bad, and does little to fundamentally change human behavior. 
>
> This text is more or less a counter argument to tech utopianism, the belief the technology will solve the world's problems. Rather, Toyama takes the perspective of a social determinist, arguing that all problems are only human problems, and that technology can only ever amplify existing human behaviors, whether those behaviors be good or bad. His arguments follow a contrary approach: he doesn't follow the economics trend of simplification, nor does he use the deeply (perhaps too deep?) contextual approach of anthropology. Surprisingly little of the book is about technology, with the former half discussing some technical interventions and the latter half turning to Toyama's experience and views with international development.  
>
> ## Structure of the book
> The first part of the book serves as a debunking of tech. utopianism, wherein Toyama draws on his experience as a tech insider (researcher/developer at Microsoft) and an educator in India and Ghana. He argues that technology has never solved any of the problems's he has seen; instead, improvement came with the help of dedicated and passionate teachers, administrators, workers, and more. Technology simply amplified the good qualities of these already good people. Toyama argues that technologies often serve as packaged interventions—something that can be moved freely between contexts with the promise of improvements. However, Toyama shows that this is not the case—packaged interventions only work when the implementers are passionate and dedicated; in other cases, packaged inerventions are either useless, harmful, or at most marginally useful. 

> The second part of the book transitions to what amounts to Toyama's views on international development and education. Toyama argues that real change comes not from packaged interventions, technology, or even really any technocratic intervention. Instead, Toyama argues for the cultivation of "heart, mind, and will" in individuals, which Toyama packages into the term "intrinsic development". He argues that national development comes from changes in individual aspirations and capacities. This view seems to in-part reconcile individualistic and collectivist views of society, and has the following general flow of though:

> - people are different, and not everyone is equally good 
> - "Heart, mind, and will" make people more good 
> - Countries which have invested in heart, mind, and will have, over time, become more > economically prosperous, free of corruption, just, and egalitarian
> - However, not everyone has had the chance or opportunities to cultivate these traits, often due to external issues (poverty, parenting, corruption, etc.). Moreover, humans tend not to naturally pursue intrinsic development (i.e.: children want to play games, not listen to class)
> - As such, successful programs must work to cultivate heart, mind in the people they are trying to help.
> - This can only happen through Mentorship: mentorship during education and guidance as an adult
>
> The second half is certaintly interesting, and I certaintly found it to be interesting and a novel perspective that I am, mostly, on board with. However, this latter half is certaintly not an academic piece, and draws heavily on Toyama's personal beliefs, though these beliefs are drawn heavily from experience. 
>
> ### Describe at least three ways that the main argument is supported.
> Toyama largely draws on personal experiences to support his point. And his experience is extensive. Currently a professor at Univeristy of Mich., Toyama has a PhD in Computer Science and has worked at Microsoft for a great deal of time, which eventually lead him to work as a teacher (still affiliated with Microsoft)in India and Africa. 
>
> The first part of the book largely draws on Toyama's experiences in these educational settings. He tells of how his initial excitement over the power of technology was misplaced. One example was MultiPoint: a simple application that allowed many children to hook a mouse into a single computer, allowing students to be engaged during computer-based lessons. However, Toyama argues that while this brought some improvement, it didn't always generalize to other contexts, and didn't cause any major improvements in children's education. He even studies Randomized Control Trials (RCTs), the gold-standard of educational and development interventions, but argues how RCTs can be inadequate for answering large complex questions and often produce marginally-useful information. 
> 
> Toyama also spends a great deal of time discussing a fair number of educational institutions, such as Ashesi University in Ghana, a univeristy that has devoted resources to training "heart, mind, and will" as Toyama puts it, and thus is investing in Africa's future. Another institution was Shanti Bhavan, a boarding school in India which enrolled children of poor and rural families and spent years cultivating virtuous traits and providing them with close mentorship. Toyama argues that each of these institutions have had imense positive impacts on the intrisic growth of their students. Moreover, these institutions didn't succeed by using fancy technologies, but rather by having dedicated staff and 
> 
> The latter half of the book continues to draw on personal experience, largely focusing on the hard-working individuals that he has met throughout his life and highlighting how their intrinsic development has contirbuted to their maturation and their turn towards socially-beneficial work, rather than just work for survival, money, or recognition.
>
> ### Describe the main literatures that the text draws on and contributes to, and the particular contribution made by the text.
>
> Toyama offers passing references to STS scholars (Latour, Turkle, etc.), economists, anthropologists, and people whom I assume are active in the field of ICT4D.
>
> ### Describe the methodology (or methodologies) used in the text, and how it enables the author(s) to support the text’s main argument.
>
> This book is based almost entirely on Toyama's personal experiences as a researcher, engineer, and a teacher, and not on a systematic methodology. He draws from personal anecdotes and the experiences of people he met along the way. As such, I don't know if this book has a "methodology" to speak of. 
>
> ### What three quotes capture the critical significance of the text?
> 
> >"Context definitely matters. All three factors, though, point to *human* context as what matters most. Or, to put it another way, the technology isn't the deciding factor even in a technology project. Of course, good design trumps poor design, but beyong some level of functionality, technical design matters much less than the human elements. The right people can work around a bad technology, but the wrong people will mess up even a good one" (pg 26)
>
> >"Of course, technologies *can* enrich lives. Voting *can* empower citizens; and microcredit *can* lead to better livelihoods. But "can" is not always "will". Modern society fetishizes technocratic devices, but it's a human finger in the on-switch and a human hand on the controls" (pg 73)
>
> > "Again, it's not that technology, packaged interventions, RCTs, social enterprises, happiness, scalability, measurability, and technocratic ideas in general are bad in and of themselves. Rather, the trouble is cultism and imbalance. New vaccines are good, but not while heal-care systems go unfunded. Educational technology might be helpful, but not if good teachers and institutional support are lacking. Elections are great, but not if social norms and government institutions don't support democracy. Technocratic means might be part of the solution, but with so much attention on them, who's working on the other parts?" (pg 99)
>
> >"Technology amplifies preexisting differences in wealth and achievement. Children with greater vocabularies gey more out of Wikipedia. Students with behavioral challenges are more distracted by video games. Rich parents will pay for tutors so that their children can learn to program the devices that others merely learn to use. Technology at school may level the playing field of access, but a level field does nothing to improve the skill of the players, which is the whole point of education. Technology by itself only increases the gap between the haves and have-nots" (pg 117)
>
> ### Relevance to my research
> ----
>
> I think that I can make use of the ideas of the "Law of amplification" and "packaged interventions" in my research. I think that Data Science offers an interesting case study for this, because it is often treated as a packaged intervention. Companies and institutions hire institutions hoping for some sort of magic to happen. However, the "magic", if it happens, is not really magic at all. Instead, following Toyama's arguments, the data science will simply amplify existing behaviors of the organization. So what does Data Science amplify? Does is amplify decision-making? human's need for classification/labeling? something else? Food for thought.s
>
> I am perosnally somewhat (though not entirely) fond of some of Toyama's ideas in the latter half of the book. I think that his philosophies serve as an interesting blend of Western focus on individualism and agency, with the more "Eastern" focus on personal virtue, community, and intrinsic development. 
