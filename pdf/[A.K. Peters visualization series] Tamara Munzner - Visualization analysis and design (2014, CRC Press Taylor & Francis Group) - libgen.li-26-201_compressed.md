What’s Vis, and Why Do It?Chapter 1
1.1 The Big Picture
This book is built around the following deﬁnition of visualization—
vis, for short:
Computer-based visualization systems provide visual
representations of datasets designed to help people carry
out tasks more effectively.
Visualization is suitable when there is a need to augment
human capabilities rather than replace people with com-putational decision-making methods. The design space
of possible vis idioms is huge, and includes the consid-
erations of both how to create and how to interact withvisual representations. Vis design is full of trade-offs, andmost possibilities in the design space are ineffective for aparticular task, so validating the effectiveness of a design
is both necessary and difﬁcult. Vis designers must take
into account three very different kinds of resource limi-tations: those of computers, of humans, and of displays.Vis usage can be analyzed in terms of why the user needsit, what data is shown, and how the idiom is designed.
I’ll discuss the rationale behind many aspects of this deﬁnition as
a way of getting you to think about the scope of this book, andabout visualization itself:
•Why have a human in the decision-making loop?
•Why have a computer in the loop?
•Why use an external representation?
•Why depend on vision?
12 1. What’s Vis, and Why Do It?
•Why show the data in detail?
•Why use interactivity?
•Why is the vis idiom design space huge?
•Why focus on tasks?
•Why are most designs ineffective?
•Why care about effectiveness?
•Why is validation difﬁcult?
•Why are there resource limitations?
•Why analyze vis?
1.2 Why Have a Human in the Loop?
Vis allows people to analyze data when they don’t know exactly
what questions they need to ask in advance.
The modern era is characterized by the promise of better deci-
sion making through access to more data than ever before. Whenpeople have well-deﬁned questions to ask about data, they can usepurely computational techniques from ﬁelds such as statistics andmachine learning.
⋆Some jobs that were once done by humans can ⋆The ﬁeld of machine
learning is a branch of
artiﬁcial intelligence where
computers can handle a
wide variety of new situa-tions in response to data-driven training, rather thanby being programmed withexplicit instructions in ad-
vance.now be completely automated with a computer-based solution. If
a fully automatic solution has been deemed to be acceptable, thenthere is no need for human judgement, and thus no need for you todesign a vis tool. For example, consider the domain of stock mar-ket trading. Currently, there are many deployed systems for high-frequency trading that make decisions about buying and sellingstocks when certain market conditions hold, when a speciﬁc priceis reached, for example, with no need at all for a time-consumingcheck from a human in the loop. You would not want to designa vis tool to help a person make that check faster, because evenan augmented human will not be able to reason about millions ofstocks every second.
However, many analysis problems are ill speciﬁed: people don’t
know how to approach the problem. There are many possible ques-tions to ask—anywhere from dozens to thousands or more—andpeople don’t know which of these many questions are the rightones in advance. In such cases, the best path forward is an anal-ysis process with a human in the loop, where you can exploit the1.2. Why Have a Human in the Loop? 3
powerful pattern detection properties of the human visual system
in your design. Vis systems are appropriate for use when your goalis to augment human capabilities, rather than completely replacethe human in the loop.
You can design vis tools for many kinds of uses. You can make
a tool intended for transitional use where the goal is to “work itselfout of a job”, by helping the designers of future solutions that arepurely computational. You can also make a tool intended for long-term use, in a situation where there is no intention of replacing the
human any time soon.
For example, you can create a vis tool that’s a stepping stone
to gaining a clearer understanding of analysis requirements beforedeveloping formal mathematical or computational models. Thiskind of tool would be used very early in the transition processin a highly exploratory way, before even starting to develop anykind of automatic solution. The outcome of designing vis toolstargeted at speciﬁc real-world domain problems is often a muchcrisper understanding of the user’s task, in addition to the toolitself.
In the middle stages of a transition, you can build a vis tool
aimed at the designers of a purely computational solution, to helpthem reﬁne, debug, or extend that system’s algorithms or under-stand how the algorithms are affected by changes of parameters.In this case, your tool is aimed at a very different audience thanthe end users of that eventual system; if the end users need vi-sualization at all, it might be with a very different interface. Re-turning to the stock market example, a higher-level system thatdetermines which of multiple trading algorithms to use in vary-ing circumstances might require careful tuning. A vis tool to helpthe algorithm developers analyze its performance might be use-ful to these developers, but not to people who eventually buy thesoftware.
You can also design a vis tool for end users in conjunction with
other computational decision making to illuminate whether the au-tomatic system is doing the right thing according to human judge-ment. The tool might be intended for interim use when makingdeployment decisions in the late stages of a transition, for exam-ple, to see if the result of a machine learning system seems to betrustworthy before entrusting it to spend millions of dollars tradingstocks. In some cases vis tools are abandoned after that decision ismade; in other cases vis tools continue to be in play with long-termuse to monitor a system, so that people can take action if they spotunreasonable behavior.4 1. What’s Vis, and Why Do It?
Figure 1.1. The Variant View vis tool supports biologists in assessing the impact
of genetic variants by speeding up the exploratory analysis process. From [Ferstay
et al. 13, Figure 1].
In contrast to these transitional uses, you can also design vis
tools for long-term use, where a person will stay in the loop indef-
initely. A common case is exploratory analysis for scientiﬁc dis-covery, where the goal is to speed up and improve a user’s abilityto generate and check hypotheses. Figure 1.1 shows a vis tooldesigned to help biologists studying the genetic basis of diseasethrough analyzing DNA sequence variation. Although these scien-tists make heavy use of computation as part of their larger work-ﬂow, there’s no hope of completely automating the process of can-cer research any time soon.
You can also design vis tools for presentation. In this case,
you’re supporting people who want to explain something that theyalready know to others, rather than to explore and analyze theunknown. For example, The New York Times has deployed sophis-
ticated interactive visualizations in conjunction with news stories.
1.3 Why Have a Computer in the Loop?
By enlisting computation, you can build tools that allow people toexplore or present large datasets that would be completely infeasi-ble to draw by hand, thus opening up the possibility of seeing howdatasets change over time.1.3. Why Have a Computer in the Loop? 5
(a)
 (b)
Figure 1.2. The Cerebral vis tool captures the style of hand-drawn diagrams in biology textbooks with vertical layers
that correspond to places within a cell where interactions between genes occur. (a) A small network of 57 nodes
and 74 edges might be possible to lay out by hand with enough patience. (b) Automatic layout handles this large
network of 760 nodes and 1269 edges and provides a substrate for interactive exploration: the user has moved themouse over the MSK1 gene, so all of its immmediate neighbors in the network are highlighted in red. From [Barsky
et al. 07, Figures 1 and 2].
People could create visual representations of datasets manu-
ally, either completely by hand with pencil and paper, or with com-
puterized drawing tools where they individually arrange and coloreach item. The scope of what people are willing and able to domanually is strongly limited by their attention span; they are un-likely to move beyond tiny static datasets. Arranging even smalldatasets of hundreds of items might take hours or days. Mostreal-world datasets are much larger, ranging from thousands tomillions to even more. Moreover, many datasets change dynami-cally over time. Having a computer-based tool generate the visualrepresentation automatically obviously saves human effort com-pared to manual creation.
As a designer, you can think about what aspects of hand-drawn
diagrams are important in order to automatically create drawingsthat retain the hand-drawn spirit. For example, Figure 1.2 shows6 1. What’s Vis, and Why Do It?
an example of a vis tool designed to show interactions between
genes in a way similar to stylized drawings that appear in biol-ogy textbooks, with vertical layers that correspond to the locationwithin the cell where the interaction occurs [Barsky et al. 07]. Fig-ure 1.2(a) could be done by hand, while Figure 1.2(b) could not.
1.4 Why Use an External Representation?
External representations augment human capacity by allowing us
to surpass the limitations of our own internal cognition and mem-ory.
Vis allows people to ofﬂoad internal cognition and memory us-
age to the perceptual system, using carefully designed images asa form of external representations , sometimes also called external
memory . External representations can take many forms, including
touchable physical objects like an abacus or a knotted string, butin this book I focus on what can be shown on the two-dimensionaldisplay surface of a computer screen.
Diagrams can be designed to support perceptual inferences,
which are very easy for humans to make. The advantages of dia-grams as external memory is that information can be organized byspatial location, offering the possibility of accelerating both searchand recognition. Search can be sped up by grouping all the itemsneeded for a speciﬁc problem-solving inference together at the samelocation. Recognition can also be facilitated by grouping all the rel-evant information about one item in the same location, avoidingthe need for matching remembered symbolic labels. However, anonoptimal diagram may group irrelevant information together, orsupport perceptual inferences that aren’t useful for the intendedproblem-solving process.
1.5 Why Depend on Vision?
Visualization, as the name implies, is based on exploiting the hu-man visual system as a means of communication. I focus exclu-sively on the visual system rather than other sensory modalitiesbecause it is both well characterized and suitable for transmittinginformation.
The visual system provides a very high-bandwidth channel to
our brains. A signiﬁcant amount of visual information processingoccurs in parallel at the preconscious level. One example is visual1.6. Why Show the Data in Detail? 7
popout, such as when one red item is immediately noticed from a
sea of gray ones. The popout occurs whether the ﬁeld of other ob-jects is large or small because of processing done in parallel acrossthe entire ﬁeld of vision. Of course, our visual systems also feedinto higher-level processes that involve the conscious control ofattention.
Sound is poorly suited for providing overviews of large informa-
tion spaces compared with vision. An enormous amount of back-
ground visual information processing in our brains underlies ourability to think and act as if we see a huge amount of information atonce, even though technically we see only a tiny part of our visualﬁeld in high resolution at any given instant. In contrast, we ex-perience the perceptual channel of sound as a sequential stream,rather than as a simultaneous experience where what we hear overa long period of time is automatically merged together. This crucialdifference may explain why soniﬁcation has never taken off despite
many independent attempts at experimentation.
The other senses can be immediately ruled out as communica-
tion channels because of technological limitations. The perceptualchannels of taste and smell don’t yet have viable recording and re-production technology at all. Haptic input and feedback devicesexist to exploit the touch and kinesthetic perceptual channels, butthey cover only a very limited part of the dynamic range of what wecan sense. Exploration of their effectiveness for communicatingabstract information is still at a very early stage.
/trianglerightsldChapter 5 covers impli-
cations of visual perception
that are relevant for vis de-sign.
1.6 Why Show the Data in Detail?
Vis tools help people in situations where seeing the dataset struc-
ture in detail is better than seeing only a brief summary of it. Oneof these situations occurs when exploring the data to ﬁnd patterns,both to conﬁrm expected ones and ﬁnd unexpected ones. Anotheroccurs when assessing the validity of a statistical model, to judgewhether the model in fact ﬁts the data.
Statistical characterization of datasets is a very powerful ap-
proach, but it has the intrinsic limitation of losing informationthrough summarization. Figure 1.3 shows Anscombe’s Quartet, a
suite of four small datasets designed by a statistician to illustratehow datasets that have identical descriptive statistics can havevery different structures that are immediately obvious when thedataset is shown graphically [Anscombe 73]. All four have identi-cal mean, variance, correlation, and linear regression lines. If you8 1. What’s Vis, and Why Do It?
1
X          Y2
X          Y3
X          Y4
X          Y
Mean
Variance
CorrelationAnscombe’s Quartet: Raw Data
Figure 1.3. Anscombe’s Quartet is four datasets with identical simple statisti-
cal properties: mean, variance, correlation, and linear regression line. However,
visual inspection immediately shows how their structures are quite different. Af-ter [Anscombe 73, Figures 1–4].1.7. Why Use Interactivity? 9
are familiar with these statistical measures, then the scatterplot of
the ﬁrst dataset probably isn’t surprising, and matches your intu-ition. The second scatterplot shows a clear nonlinear pattern inthe data, showing that summarizing with linear regression doesn’tadequately capture what’s really happening. The third datasetshows how a single outlier can lead to a regression line that’s mis-leading in a different way because its slope doesn’t quite matchthe line that our eyes pick up clearly from the rest of the data.Finally, the fourth dataset shows a truly pernicious case wherethese measures dramatically mislead, with a regression line that’salmost perpendicular to the true pattern we immediately see inthe data.
The basic principle illustrated by Anscombe’s Quartet, that a
single summary is often an oversimpliﬁcation that hides the truestructure of the dataset, applies even more to large and complexdatasets.
1.7 Why Use Interactivity?
Interactivity is crucial for building vis tools that handle complex-ity. When datasets are large enough, the limitations of both peopleand displays preclude just showing everything at once; interac-
tion where user actions cause the view to change is the way for-
ward. Moreover, a single static view can show only one aspect ofa dataset. For some combinations of simple datasets and tasks,the user may only need to see a single visual encoding. In con-trast, an interactively changing display supports many possiblequeries.
In all of these cases, interaction is crucial. For example, an in-
teractive vis tool can support investigation at multiple levels of de-
tail, ranging from a very high-level overview down through multiple
levels of summarization to a fully detailed view of a small part of it.It can also present different ways of representing and summariz-ing the data in a way that supports understanding the connectionsbetween these alternatives.
Before the widespread deployment of fast computer graphics,
visualization was limited to the use of static images on paper. Withcomputer-based vis, interactivity becomes possible, vastly increas-ing the scope and capabilities of vis tools. Although static repre-sentations are indeed within the scope of this book, interaction isan intrinsic part of many idioms.10 1. What’s Vis, and Why Do It?
1.8 Why Is the Vis Idiom Design Space Huge?
A vis idiom is a distinct approach to creating and manipulating
visual representations. There are many ways to create a visual en-
coding of data as a single picture. The design space of possibilities
gets even bigger when you consider how to manipulate one or more
of these pictures with interaction .
Many vis idioms have been proposed. Simple static idioms in-
clude many chart types that have deep historical roots, such asscatterplots, bar charts, and line charts. A more complicated id-iom can link together multiple simple charts through interaction.For example, selecting one bar in a bar chart could also result inhighlighting associated items in a scatterplot that shows a differ-ent view of the same data. Figure 1.4 shows an even more com-plex idiom that supports incremental layout of a multilevel networkthrough interactive navigation. Data from Internet Movie Databaseshowing all movies connected to Sharon Stone is shown, where ac-tors are represented as grey square nodes and links between them
Figure 1.4. The Grouse vis tool features a complex idiom that combines visual
encoding and interaction, supporting incremental layout of a network through in-
teractive navigation. From [Archambault et al. 07a, Figure 5].1.9. Why Focus on T asks? 11
mean appearance in the same movie. The user has navigated by
opening up several metanodes, shown as discs, to see structure atmany levels of the hierarchy simultaneously; metanode color en-codes the topological structure of the network features it contains,and hexagons indicate metanodes that are still closed. The insetshows the details of the opened-up clique of actors who all appearin the movie Anything but Here , with name labels turned on.
/trianglerightsldCompound networks are
discussed further in Sec-
tion 9.5.
This book provides a framework for thinking about the space
of vis design idioms systematically by considering a set of design
choices, including how to encode information with spatial position,how to facet data between multiple views, and how to reduce theamount of data shown by ﬁltering and aggregation.
1.9 Why Focus on T asks?
A tool that serves well for one task can be poorly suited for another,for exactly the same dataset. The task of the users is an equallyimportant constraint for a vis designer as the kind of data that theusers have.
Reframing the users’ task from domain-speciﬁc form into ab-
stract form allows you to consider the similarities and differencesbetween what people need across many real-world usage contexts.For example, a vis tool can support presentation, or discovery, orenjoyment of information; it can also support producing more in-formation for subsequent use. For discovery, vis can be used togenerate new hypotheses, as when exploring a completely unfamil-iar dataset, or to conﬁrm existing hypotheses about some datasetthat is already partially understood.
/trianglerightsldThe space of task ab-
stractions is discussed in
detail in Chapter 3.
1.10 Why Focus on Effectiveness?
The focus on effectiveness is a corollary of deﬁning vis to have the
goal of supporting user tasks. This goal leads to concerns aboutcorrectness, accuracy, and truth playing a very central role in vis.The emphasis in vis is different from other ﬁelds that also involvemaking images: for example, art emphasizes conveying emotion,
achieving beauty, or provoking thought; movies and comics em-phasize telling a narrative story; advertising emphasizes setting amood or selling. For the goals of emotional engagement, story-telling, or allurement, the deliberate distortion and even fabrica-tion of facts is often entirely appropriate, and of course ﬁction is as12 1. What’s Vis, and Why Do It?
respectable as nonﬁction. In contrast, a vis designer does not typi-
cally have artistic license. Moreover, the phrase “it’s not just aboutmaking pretty pictures” is a common and vehement assertion invis, meaning that the goals of the designer are not met if the resultis beautiful but not effective.
However, no picture can communicate the truth, the whole truth,
and nothing but the truth. The correctness concerns of a vis de-signer are complicated by the fact that any depiction of data is
an abstraction where choices are made about which aspects toemphasize. Cartographers have thousands of years of experience
/trianglerightsldAbstraction is discussed
in more detail in Chapters 3
and 4.with articulating the difference between the abstraction of a map
and the terrain that it represents. Even photographing a real-worldscene involves choices of abstraction and emphasis; for example,the photographer chooses what to include in the frame.
1.11 Why Are Most Designs Ineffective?
The most fundamental reason that vis design is a difﬁcult enter-prise is that the vast majority of the possibilities in the design spacewill be ineffective for any speciﬁc usage context. In some cases, apossible design is a poor match with the properties of the humanperceptual and cognitive systems. In other cases, the design wouldbe comprehensible by a human in some other setting, but it’s a badmatch with the intended task. Only a very small number of pos-sibilities are in the set of reasonable choices, and of those onlyan even smaller fraction are excellent choices. Randomly choosingpossibilities is a bad idea because the odds of ﬁnding a very goodsolution are very low.
Figure 1.5 contrasts two ways to think about design in terms of
traversing a search space. In addressing design problems, it’s nota very useful goal to optimize ; that is, to ﬁnd the very best choice. A
more appropriate goal when you design is to satisfy ; that is, to ﬁnd
one of the many possible good solutions rather than one of the evenlarger number of bad ones. The diagram shows ﬁve spaces, eachof which is progressively smaller than the previous. First, thereis the space of all possible solutions, including potential solutionsthat nobody has ever thought of before. Next, there is the set ofpossibilities that are known to you, the vis designer. Of course,
this set might be small if you are a novice designer who is notaware of the full array of methods that have been proposed in thepast. If you’re in that situation, one of the goals of this book is toenlarge the set of methods that you know about. The next set is the1.11. Why Are Most Designs Ineffective? 13
xConsideration 
spaceProposal 
space
xBad!
xxxx
ooo
x o
oGood!
Space of possible solutionsKnown 
spaceSelected
solution 
x
Good solutionOK solutionPoor Solutionx
o
Space of possible solutionsox
oo
ooo
oo
o
Figure 1.5. A search space metaphor for vis design.
consideration space, which contains the solutions that you actively
consider. This set is necessarily smaller than the known space,
because you can’t consider what you don’t know. An even smallerset is the proposal space of possibilities that you investigate in
detail. Finally, one of these becomes the selected solution.
Figure 1.5 contrasts a good strategy on the left, where the known
and consideration spaces are large, with a bad strategy on theright, where these spaces are small. The problem of a small con-sideration space is the higher probability of only considering okor poor solutions and missing a good one. A fundamental princi-ple of design is to consider multiple alternatives and then choosethe best, rather than to immediately ﬁxate on one solution withoutconsidering any alternatives. One way to ensure that more thanone possibility is considered is to explicitly generate multiple ideasin parallel. This book is intended to help you, the designer, en-tertain a broad consideration space by systematically consideringmany alternatives and to help you rule out some parts of the spaceby noting when there are mismatches of possibilities with humancapabilities or the intended task.
As with all design problems, vis design cannot be easily handled
as a simple process of optimization because trade-offs abound. Adesign that does well by one measure will rate poorly on another.The characterization of trade-offs in the vis design space is a veryopen problem at the frontier of vis research. This book providesseveral guidelines and suggested processes, based on my synthesisof what is currently known, but it contains few absolute truths.
/trianglerightsldChapter 4 introduces a
model for thinking about
the design process at fourdifferent levels; the modelis intended to guide your
thinking through thesetrade-offs in a systematicway.14 1. What’s Vis, and Why Do It?
1.12 Why Is Validation Difﬁcult?
The problem of validation for a vis design is difﬁcult because there
are so many questions that you could ask when considering whether
a vis tool has met your design goals.
How do you know if it works? How do you argue that one de-
sign is better or worse than another for the intended users? For
one thing, what does better mean? Do users get something done
faster? Do they have more fun doing it? Can they work more effec-tively? What does effectively mean? How do you measure insight
orengagement ? What is the design better than? Is it better than
another vis system? Is it better than doing the same things man-ually, without visual support? Is it better than doing the samethings completely automatically? And what sort of thing does itdo better? That is, how do you decide what sort of task the usersshould do when testing the system? And who is this user ? An ex-
pert who has done this task for decades, or a novice who needs thetask to be explained before they begin? Are they familiar with howthe system works from using it for a long time, or are they seeingit for the ﬁrst time? A concept like faster might seem straightfor-
ward, but tricky questions still remain. Are the users limited bythe speed of their own thought process, or their ability to movethe mouse, or simply the speed of the computer in drawing eachpicture?
How do you decide what sort of benchmark data you should
use when testing the system? Can you characterize what classesof data the system is suitable for? How might you measure thequality of an image generated by a vis tool? How well do any of
the automatically computed quantitative metrics of quality matchup with human judgements? Even once you limit your considera-tions to purely computational issues, questions remain. Does thecomplexity of the algorithm depend on the number of data items toshow or the number of pixels to draw? Is there a trade-off betweencomputer speed and computer memory usage?
/trianglerightsldChapter 4 answers these
questions by providing a
framework that addresses
when to use what methodsfor validating vis designs.
1.13 Why Are There Resource Limitations?
When designing or analyzing a vis system, you must consider at
least three different kinds of limitations: computational capacity,human perceptual and cognitive capacity, and display capacity.
Vis systems are inevitably used for larger datasets than those
they were designed for. Thus, scalability is a central concern: de-1.13. Why Are There Resource Limitations? 15
signing systems to handle large amounts of data gracefully. The
continuing increase in dataset size is driven by many factors: im-provements in data acquisition and sensor technology, bringingreal-world data into a computational context; improvements incomputer capacity, leading to ever-more generation of data fromwithin computational environments including simulation and log-ging; and the increasing reach of computational infrastructure intoevery aspect of life.
As with any application of computer science, computer time and
memory are limited resources, and there are often soft and hardconstraints on the availability of these resources. For instance, ifyour vis system needs to interactively deliver a response to user in-put, then when drawing each frame you must use algorithms thatcan run in a fraction of a second rather than minutes or hours. In
some scenarios, users are unwilling or unable to wait a long timefor the system to preprocess the data before they can interact withit. A soft constraint is that the vis system should be parsimoniousin its use of computer memory because the user needs to run otherprograms simultaneously. A hard constraint is that even if thevis system can use nearly all available memory in the computer,dataset size can easily outstrip that ﬁnite capacity. Designing sys-tems that gracefully handle larger datasets that do not ﬁt into corememory requires signiﬁcantly more complex algorithms. Thus, thecomputational complexity of algorithms for dataset preprocessing,transformation, layout, and rendering is a major concern. How-ever, computational issues are by no means the only concern!
On the human side, memory and attention are ﬁnite resources.
Chapter 5 will discuss some of the power and limitations of thelow-level visual preattentive mechanisms that carry out massivelyparallel processing of our current visual ﬁeld. However, humanmemory for things that are not directly visible is notoriously lim-ited. These limits come into play not only for long-term recall butalso for shorter-term working memory, both visual and nonvisual.We store surprisingly little information internally in visual work-ing memory, leaving us vulnerable to change blindness : the phe-
nomenon where even very large changes are not noticed if we areattending to something else in our view [Simons 00].
/trianglerightsldMore aspects of memory
and attention are covered in
Section 6.5.
Display capacity is a third kind of limitation to consider. Vis de-
signers often run out of pixels; that is, the resolution of the screen
is not enough to show all desired information simultaneously. Theinformation density of a single image is a measure of the amount
of information encoded versus the amount of unused space.
⋆Fig-⋆Synonyms for informa-
tion density include gra-
phic density and data–ink
ratio . ure 1.6 shows the same tree dataset visually encoded three differ-16 1. What’s Vis, and Why Do It?
(a)
(b) (c)
Figure 1.6. Low and high information density visual encodings of the same small
tree dataset; nodes are the same size in each. (a) Low information density. (b)
Higher information density, but depth in tree cannot be read from spatial position.(c) High information density, while maintaining property that depth is encoded with
position. From [McGufﬁn and Robert 10, Figure 3].
ent ways. The layout in Figure 1.6(a) encodes the depth from root
to leaves in the tree with vertical spatial position. However, theinformation density is low. In contrast, the layout in Figure 1.6(b)uses nodes of the same size but is drawn more compactly, so ithas higher information density; that is, the ratio between the sizeof each node and the area required to display the entire tree islarger. However, the depth cannot be easily read off from spatialposition. Figure 1.6(c) shows a very good alternative that combinesthe beneﬁts of both previous approaches, with both high informa-tion density from a compact view and position coding for depth.
There is a trade-off between the beneﬁts of showing as much
as possible at once, to minimize the need for navigation and explo-ration, and the costs of showing too much at once, where the useris overwhelmed by visual clutter. The goal of idiom design choicesis to ﬁnd an appropriate balance between these two ends of theinformation density continuum.
1.14 Why Analyze?
This book is built around the premise that analyzing existing sys-tems is a good stepping stone to designing new ones. When you’reconfronted with a vis problem as a designer, it can be hard to de-cide what to do. Many computer-based vis idioms and tools have1.14. Why Analyze? 17
Why?
How?What?
Figure 1.7. Three-part analysis framework for a vis instance: why is the task being
performed, what data is shown in the views, and how is the vis idiom constructed
in terms of design choices.
been created in the past several decades, and considering them
one by one leaves you faced with a big collection of different pos-sibilities. There are so many possible combinations of data, tasks,and idioms that it’s unlikely that you’ll ﬁnd exactly what you needto know just by reading papers about previous vis tools. More-over, even if you ﬁnd a likely candidate, you might need to digeven deeper into the literature to understand whether there’s anyevidence that the tool was a success.
This book features an analysis framework that imposes a struc-
ture on this enormous design space, intended as a scaffold to helpyou think about design choices systematically. It’s offered as aguide to get you started, not as a straitjacket: there are certainlymany other possible ways to think about these problems!
Figure 1.7 shows the high-level framework for analyzing vis use
according to three questions: what data the user sees, why the
user intends to use a vis tool, and how the visual encoding and in-
teraction idioms are constructed in terms of design choices. Eachthree-fold what–why–how question has a corresponding data–task–
idiom answer trio. One of these analysis trios is called an instance .
/trianglerightsldChapter 2 discusses data
and the question of what .
Chapter 3 covers tasks and
the question of why . Chap-
ters 7 through 14 answerthe question of how idioms
can be designed in detail.Simple vis tools can be fully described as an isolated analy-
sis instance, but complex vis tool usage often requires analysis
in terms of a sequence of instances that are chained together. Inthese cases, the chained sequences are a way to express dependen-cies. All analysis instances have the input ofwhat data is shown;
in some cases, output data is produced as a result of using the
vis tool. Figure 1.8 shows an abstract example of a chained se-quence, where the output of a prior instance serves as the input toa subsequent one.
The combination of distinguishing why from how and chained
sequences allows you to distinguish between means and ends in18 1. What’s Vis, and Why Do It?
Why?
How?
 What?Why?
How?
 What?Why?
How?
 What?
Figure 1.8. Analyzing vis usage as chained sequences of instances, where the
output of one instance is the input to another.
your analysis. For example, a user could sort the items shown
within the vis. That operation could be an end in itself, if the user’sgoal is to produce a list of items ranked according to a particularcriterion as a result of an analysis session. Or, the sorting could bethe means to another end, for example, ﬁnding outliers that do notmatch the main trend of the data; in this case, it is simply donealong the way as one of many different operations.
1.15 Further Reading
Each Further Reading section provides suggestions for further read-ing about some of the ideas presented in the chapter and acknowl-edges key sources that inﬂuenced the discussion.
Why Use an External Representation? The role and use of external
representations are analyzed in papers on the nature of ex-1.15. Further Reading 19
ternal representations in problem solving [Zhang 97] and a
representational analysis of number systems [Zhang and Nor-man 95]. The inﬂuential paper Why A Diagram Is (Sometimes)
Worth Ten Thousand Words is the basis for my discussion of
diagrams in this chapter [Larkin and Simon 87].
Why Show the Data in Detail? Anscombe proposed his quartet of illus-
trative examples in a lovely, concise paper [Anscombe 73]. Anearly paper on the many faces of the scatterplot includes a
cogent discussion of why to show as much of the data as pos-sible [Cleveland and McGill 84b].
What Is the Vis Design Space? My discussion of the vis design space
is based on our paper on the methodology of design studiesthat covers the question of progressing from a loose to a crispunderstanding of the user’s requirements [Sedlmair et al. 12].
What Resource Limitations Matter? Ware’s textbook provides a very thor-
ough discussion of human limitations in terms of perception,memory, and cognition [Ware 13]. A survey paper provides agood overview of the change blindness literature [Simons 00].
The idea of information density dates back to Bertin’s discus-
sion of graphic density [Bertin 67], and Tufte has discussed
the data–ink ratio at length [Tufte 83].Why?
How?What?DatasetsWhat?
Attributes
Dataset TypesData Types
Data and Dataset Types
Dataset Availability
Static DynamicTables
Attributes (columns)
Items 
(rows)
Cell containing valueNetworks
Link
Node 
(item)
TreesFields (Continuous)
Geometry (Spatial)Attributes (columns)
Value in cellCell
Multidimensional Table
Value in cellItems Attributes Links Positions GridsAttribute Types
Ordering DirectionCategorical
Ordered
Ordinal
Quantitative
Sequential
Diverging
CyclicTables Networks & 
TreesFields Geometry Clusters, 
Sets, Lists
Items
AttributesItems (nodes)
Links
AttributesGrids
Positions
AttributesItems
PositionsItems
Grid of positions
Position
Figure 2.1. What can be visualized: data, datasets, and attributes.What: Data AbstractionChapter 2
2.1 The Big Picture
Figure 2.1 shows the abstract types of what can be visualized. The
four basic dataset types are tables, networks, ﬁelds, and geome-
try; other possible collections of items include clusters, sets, andlists. These datasets are made up of different combinations of theﬁve data types: items, attributes, links, positions, and grids. Forany of these dataset types, the full dataset could be available im-mediately in the form of a static ﬁle, or it might be dynamic dataprocessed gradually in the form of a stream. The type of an at-tribute can be categorical or ordered, with a further split into or-dinal and quantitative. The ordering direction of attributes can besequential, diverging, or cyclic.
2.2 Why Do Data Semantics
and T ypes Matter?
Many aspects of vis design are driven by the kind of data that you
have at your disposal. What kind of data are you given? Whatinformation can you ﬁgure out from the data, versus the meaningsthat you must be told explicitly? What high-level concepts willallow you to split datasets apart into general and useful pieces?
Suppose that you see the following data:
14, 2.6, 30, 30, 15, 100001
What does this sequence of six numbers mean? You can’t pos-
sibly know yet, without more information about how to interpret
each number. Is it locations for two points far from each otherin three-dimensional space, 14,2.6,30and 30,15,100001 ? Is it two
points closer to each other in two-dimensional space, 14,2.6and
2122 2. What: Data Abstraction
30,30, with the ﬁfth number meaning that there are 15 links be-
tween these two points, and the sixth number assigning the weight
of ‘100001’ to that link?
Similarly, suppose that you see the following data:
Basil, 7, S, Pear
These numbers and words could have many possible meanings.
Maybe a food shipment of produce has arrived in satisfactory con-dition on the 7th day of the month, containing basil and pears.Maybe the Basil Point neighborhood of the city has had 7 inchesof snow cleared by the Pear Creek Limited snow removal service.Maybe the lab rat named Basil has made seven attempts to ﬁndhis way through the south section of the maze, lured by scent ofthe reward food for this trial, a pear.
To move beyond guesses, you need to know two crosscutting
pieces of information about these terms: their semantics and theirtypes. The semantics of the data is its real-world meaning. For
instance, does a word represent a human ﬁrst name, or is it the
shortened version of a company name where the full name can belooked up in an external list, or is it a city, or is it a fruit? Does anumber represent a day of the month, or an age, or a measurementof height, or a unique code for a speciﬁc person, or a postal codefor a neighborhood, or a position in space?
The type of the data is its structural or mathematical interpre-
tation. At the data level, what kind of thing is it: an item, a link, anattribute? At the dataset level, how are these data types combinedinto a larger structure: a table, a tree, a ﬁeld of sampled values?At the attribute level, what kinds of mathematical operations aremeaningful for it? For example, if a number represents a count ofboxes of detergent, then its type is a quantity, and adding two suchnumbers together makes sense. If the number represents a postalcode, then its type is a code rather than a quantity —it is simply
the name for a category that happens to be a number rather than
a textual name. Adding two of these numbers together does notmake sense.
Table 2.1 shows several more lines of the same dataset. This
simple example table is tiny, with only nine rows and four columns.The exact semantics should be provided by the creator of the data-set; I give it with the column titles. In this case, each person has aunique identiﬁer, a name, an age, a shirt size, and a favorite fruit.
Sometimes types and semantics can be correctly inferred simply
by observing the syntax of a data ﬁle or the names of variables2.3. Data T ypes 23
ID Name Age Shirt Size Favorite Fruit
1 Amy 8 S Apple
2 Basil 7 S Pear3 Clara 9 M Durian4 Desmond 13 L Elderberry5 Ernest 12 L Peach6 Fanny 10 S Lychee7 George 9 M Orange8 Hector 8 L Loquat9 Ida 10 M Pear10 Amy 12 M Orange
Table 2.1. A full table with column titles that provide the intended semantics of the
attributes.
within it, but often they must be provided along with the dataset
in order for it to be interpreted correctly. Sometimes this kind ofadditional information is called metadata ; the line between data
and metadata is not clear, especially given that the original datais often derived and transformed. In this book, I don’t distinguish
/trianglerightsldDeriving data is dis-
cussed in Section 3.4.2.3.
between them, and refer to everything as data .
The classiﬁcation below presents a way to think about dataset
and attribute types and semantics in a way that is general enoughto cover the cases interesting in vis, yet speciﬁc enough to be help-ful for guiding design choices at the abstraction and idiom levels.
2.3 Data T ypes
Figure 2.2 shows the ﬁve basic data types discussed in this book:
items, attributes, links, positions, and grids. An attribute is some
speciﬁc property that can be measured, observed, or logged.⋆For⋆Synonyms for attribute
are variable and data di-
mension , or just dimen-
sion for short. Since dimen-
sion has many meanings, in
this book it is reserved for
the visual channels of spa-
tial position as discussed inSection 6.3.example, attributes could be salary, price, number of sales, pro-
tein expression levels, or temperature. An item is an individual
entity that is discrete, such as a row in a simple table or a node
Data Types
Items Attributes Links Positions Grids
Figure 2.2. The ﬁve basic data types: items, attributes, links, positions, and grids.24 2. What: Data Abstraction
in a network. For example, items may be people, stocks, coffee
shops, genes, or cities. A link is a relationship between items, typ-
ically within a network. A grid speciﬁes the strategy for sampling
continuous data in terms of both geometric and topological rela-tionships between its cells. A position is spatial data, providing a
location in two-dimensional (2D) or three-dimensional (3D) space.For example, a position might be a latitude–longitude pair describ-ing a location on the Earth’s surface or three numbers specifying alocation within the region of space measured by a medical scanner.
2.4 Dataset T ypes
Adataset is any collection of information that is the target of anal-
ysis.⋆The four basic dataset types are tables, networks, ﬁelds, and⋆The word dataset is sin-
gular. In vis the word data
is commonly used as a sin-
gular mass noun as well,in contrast to the traditionalusage in the natural sci-ences where data is plural.geometry. Other ways to group items together include clusters,
sets, and lists. In real-world situations, complex combinations ofthese basic types are common.
Figure 2.3 shows that these basic dataset types arise from com-
binations of the data types of items, attributes, links, positions,and grids.
Figure 2.4 shows the internal structure of the four basic dataset
types in detail. Tables have cells indexed by items and attributes,for either the simple ﬂat case or the more complex multidimen-sional case. In a network, items are usually called nodes, andthey are connected with links; a special case of networks is trees.Continuous ﬁelds have grids based on spatial positions where cellscontain attributes. Spatial geometry has only position information.
Data and Dataset Types
Tables Networks & 
TreesFields Geometry Clusters, 
Sets, Lists
Items
AttributesItems (nodes)
Links
AttributesGrids
Positions
AttributesItems
PositionsItems
Figure 2.3. The four basic dataset types are tables, networks, ﬁelds, and geome-
try; other possible collections of items are clusters, sets, and lists. These datasets
are made up of ﬁve core data types: items, attributes, links, positions, and grids.2.4. Dataset T ypes 25
Tables
Attributes (columns)
Items 
(rows)
Cell containing valueNetworks
Link
Node 
(item)
TreesFields (Continuous)
Attributes (columns)
Value in cellCell
Multidimensional Table
Value in cellGrid of positionsGeometry (Spatial)
PositionDataset Types
Figure 2.4. The detailed structure of the four basic dataset types.
2.4.1 T ables
Many datasets come in the form of tables that are made up of
rows and columns, a familiar form to anybody who has used aspreadsheet. In this chapter, I focus on the concept of a table assimply a type of dataset that is independent of any particular visualrepresentation; later chapters address the question of what visualrepresentations are appropriate for the different types of datasets.
/trianglerightsldChapter 7 covers how to
arrange tables spatially.
For a simple ﬂat table , the terms used in this book are that each
row represents an item of data, and each column is an attribute of
the dataset. Each cell in the table is fully speciﬁed by the com-
bination of a row and a column—an item and an attribute—andcontains a value for that pair. Figure 2.5 shows an example of
the ﬁrst few dozen items in a table of orders, where the attributesare order ID, order date, order priority, product container, productbase margin, and ship date.
Amultidimensional table has a more complex structure for in-
dexing into a cell, with multiple keys./trianglerightsldKeys and values are
discussed further in Sec-
tion 2.6.1.26 2. What: Data Abstraction
20
Fieldattribute
item cell
Figure 2.5. In a simple table of orders, a row represents an item , a column rep-
resents an attribute , and their intersection is the cell containing the value for that
pairwise combination.
2.4.2 Networks and T rees
The dataset type of networks is well suited for specifying that there
is some kind of relationship between two or more items.⋆An item in⋆A synonym for networks
isgraphs . The word graph
is also deeply overloaded in
vis. Sometimes it is usedto mean network as we dis-
cuss here, for instance in
the vis subﬁeld called graph
drawing or the mathemat-
ical subﬁeld called graph
theory . Sometimes it is
used in the ﬁeld of statisti-cal graphics to mean chart ,
as in bar graphs and line
graphs.a network is often called a node .⋆Alink is a relation between two
⋆A synonym for node is
vertex .items.⋆For example, in an articulated social network the nodes
⋆A synonym for link is
edge .are people, and links mean friendship. In a gene interaction net-
work, the nodes are genes, and links between them mean thatthese genes have been observed to interact with each other. In acomputer network, the nodes are computers, and the links repre-sent the ability to send messages directly between two computers
using physical cables or a wireless connection.
Network nodes can have associated attributes, just like items in
a table. In addition, the links themselves could also be consideredto have attributes associated with them; these may be partly orwholly disjoint from the node attributes.2.4. Dataset T ypes 27
It is again important to distinguish between the abstract con-
cept of a network and any particular visual layout of that network
where the nodes and edges have particular spatial positions. Thischapter concentrates on the former./trianglerightsldThe spatial arrangement
of networks is covered in
Chapter 9.
2.4.2.1 T rees
Networks with hierarchical structure are more speciﬁcally called
trees . In contrast to a general network, trees do not have cycles:
each child node has only one parent node pointing to it. One exam-ple of a tree is the organization chart of a company, showing whoreports to whom; another example is a tree showing the evolu-tionary relationships between species in the biological tree of life,where the child nodes of humans and monkeys both share thesame parent node of primates.
2.4.3 Fields
The ﬁeld dataset type also contains attribute values associated
with cells.1Each cell in a ﬁeld contains measurements or calcula-
tions from a continuous domain: there are conceptually inﬁnitely
many values that you might measure, so you could always takea new measurement between any two existing ones. Continuousphenomena that might be measured in the physical world or simu-lated in software include temperature, pressure, speed, force, anddensity; mathematical functions can also be continuous.
For example, consider a ﬁeld dataset representing a medical
scan of a human body containing measurements indicating thedensity of tissue at many sample points, spread regularly through-out a volume of 3D space. A low-resolution scan would have262,144 cells, providing information about a cubical volume ofspace with 64 bins in each direction. Each cell is associated witha speciﬁc region in 3D space. The density measurements couldbe taken closer together with a higher resolution grid of cells, orfurther apart for a coarser grid.
Continuous data requires careful treatment that takes into ac-
count the mathematical questions of sampling , how frequently to
1My use of the term ﬁeld is related to but not identical to its use in the math-
ematics literature, where it denotes a mapping from a domain to a range. In this
case, the domain is a Euclidean space of one, two, or three dimensions, and the ad-jective modifying ﬁeld is a statement about the range: scalars ,vectors ,o r tensors .
Although the term ﬁeld by itself is not commonly found in the literature, when I
use it without an adjective I’m emphasizing the continuous nature of the domain,rather than speciﬁcs of the ranges of scalars, vectors, or tensors.28 2. What: Data Abstraction
take the measurements, and interpolation , how to show values in
between the sampled points in a way that does not mislead. In-
terpolating appropriately between the measurements allows youtoreconstruct a new view of the data from an arbitrary viewpoint
that’s faithful to what you measured. These general mathematicalproblems are studied in areas such as signal processing and statis-tics. Visualizing ﬁelds requires grappling extensively with theseconcerns.
In contrast, the table and network datatypes discussed above
are an example of discrete data where a ﬁnite number of individ-
ual items exist, and interpolation between them is not a mean-ingful concept. In the cases where a mathematical framework isnecessary, areas such as graph theory and combinatorics providerelevant ideas.
2
2.4.3.1 Spatial Fields
Continuous data is often found in the form of a spatial ﬁeld , where
the cell structure of the ﬁeld is based on sampling at spatial po-sitions. Most datasets that contain inherently spatial data occurin the context of tasks that require understanding aspects of itsspatial structure, especially shape.
For example, with a spatial ﬁeld dataset that is generated with a
medical imaging instrument, the user’s task could be to locate sus-pected tumors that can be recognized through distinctive shapes ordensities. An obvious choice for visual encoding would be to showsomething that spatially looks like an X-ray image of the humanbody and to use color coding to highlight suspected tumors. An-other example is measurements made in a real or simulated windtunnel of the temperature and pressure of air ﬂowing over airplanewings at many points in 3D space, where the task is to comparethe ﬂow patterns in different regions. One possible visual encod-ing would use the geometry of the wing as the spatial substrate,showing the temperature and pressure using size-coded arrows.
The likely tasks faced by users who have spatial ﬁeld data con-
strains many of the choices about the use of space when designingvisual encoding idioms. Many of the choices for nonspatial data ,
where no information about spatial position is provided with thedataset, are unsuitable in this case.
⋆⋆A synonym for nonspatial
data isabstract data .
2Technically, all data stored within a computer is discrete rather than continu-
ous; however, the interesting question is whether the underlying semantics of the
bits that are stored represents samples of a continuous phenomenon or intrinsically
discrete data.2.4. Dataset T ypes 29
Thus, the question of whether a dataset has the type of a spa-
tial ﬁeld or a nonspatial table has extensive and far-reaching im-
plications for idiom design. Historically, vis diverged into areas ofspecialization based on this very differentiation. The subﬁeld ofscientiﬁc visualization ,o r scivis for short, is concerned with situ-
ations where spatial position is given with the dataset. A central
concern in scivis is handling continuous data appropriately withinthe mathematical framework of signal processing. The subﬁeld ofinformation visualization ,o r infovis for short, is concerned with sit-
uations where the use of space in a visual encoding is chosen by
the designer. A central concern in infovis is determining whetherthe chosen idiom is suitable for the combination of data and task,leading to the use of methods from human–computer interactionand design.
2.4.3.2 Grid T ypes
When a ﬁeld contains data created by sampling at completely reg-ular intervals, as in the previous example, the cells form a uniform
grid . There is no need to explicitly store the grid geometry in terms
of its location in space, or the grid topology in terms of how each
cell connects with its neighboring cells. More complicated exam-ples require storing different amounts of geometric and topologicalinformation about the underlying grid. A rectilinear grid supports
nonuniform sampling, allowing efﬁcient storage of information that
has high complexity in some areas and low complexity in others, atthe cost of storing some information about the geometric location ofeach each row. A structured grid allows curvilinear shapes, where
the geometric location of each cell needs to be speciﬁed. Finally,unstructured grids provide complete ﬂexibility, but the topological
information about how the cells connect to each other must bestored explicitly in addition to their spatial positions.
2.4.4 Geometry
The geometry dataset type speciﬁes information about the shape
of items with explicit spatial positions. The items could be points,or one-dimensional lines or curves, or 2D surfaces or regions, or3D volumes.
Geometry datasets are intrinsically spatial, and like spatial ﬁelds
they typically occur in the context of tasks that require shape un-derstanding. Spatial data often includes hierarchical structure atmultiple scales. Sometimes this structure is provided intrinsically30 2. What: Data Abstraction
with the dataset, or a hierarchy may be derived from the original
data.
Geometry datasets do not necessarily have attributes, in con-
trast to the other three basic dataset types. Many of the designissues in vis pertain to questions about how to encode attributes.Purely geometric data is interesting in a vis context only when itis derived or transformed in a way that requires consideration ofdesign choices. One classic example is when contours are derived
/trianglerightsldSection 3.4.2.3 covers
deriving data.
from a spatial ﬁeld. Another is when shapes are generated at an
/trianglerightsldSection 8.4 covers gen-
erating contours from scalar
ﬁelds.appropriate level of detail for the task at hand from raw geographic
data, such as the boundaries of a forest or a city or a country, orthe curve of a road. The problem of how to create images from a ge-ometric description of a scene falls into another domain: computergraphics. While vis draws on algorithms from computer graphics,it has different concerns from that domain. Simply showing a geo-metric dataset is not an interesting problem from the point of viewof a vis designer.
Geometric data is sometimes shown alone, particularly when
shape understanding is the primary task. In other cases, it is thebackdrop against which additional information is overlaid.
2.4.5 Other Combinations
Beyond tables, there are many ways to group multiple items to-
gether, including sets, lists, and clusters. A set is simply an un-
ordered group of items. A group of items with a speciﬁed orderingcould be called a list.
⋆Acluster is a grouping based on attribute ⋆In computer science, ar-
ray is often used as a syn-
onym for list.similarity, where items within a cluster are more similar to eachother than to ones in another cluster.
There are also more complex structures built on top of the basic
network type. A path through a network is an ordered set of seg-
ments formed by links connecting nodes. A compound network is
a network with an associated tree: all of the nodes in the networkare the leaves of the tree, and interior nodes in the tree provide ahierarchical structure for the nodes that is different from networklinks between them.
Many other kinds of data either ﬁt into one of the previous cat-
egories or do so after transformations to create derived attributes.Complex and hybrid combinations, where the complete datasetcontains multiple basic types, are common in real-world applica-tions.
The set of basic types presented above is a starting point for
describing the what part of an analysis instance that pertains to2.5. Attribute T ypes 31
Dataset Availability
Static Dynamic
Figure 2.6. Dataset availability can be either static or dynamic, for any dataset
type.
data; that is, the data abstraction . In simple cases, it may be possi-
ble to describe your data abstraction using only that set of terms.
In complex cases, you may need additional description as well.If so, your goal should be to translate domain-speciﬁc terms intowords that are as generic as possible.
2.4.6 Dataset Availability
Figure 2.6 shows the two kinds of dataset availability: static or
dynamic .
The default approach to vis assumes that the entire dataset is
available all at once, as a static ﬁle . However, some datasets are
instead dynamic streams , where the dataset information trickles in
over the course of the vis session.⋆One kind of dynamic change is ⋆A synonym for dynamic
isonline , and a synonym
forstatic isofﬂine .to add new items or delete previous items. Another is to changethe values of existing items.
This distinction in availability crosscuts the basic dataset types:
any of them can be static or dynamic. Designing for streamingdata adds complexity to many aspects of the vis process that arestraightforward when there is complete dataset availability up front.
2.5 Attribute T ypes
Figure 2.7 shows the attribute types. The major disinction is be-tween categorical versus ordered. Within the ordered type is afurther differentiation between ordinal versus quantitative. Or-dered data might range sequentially from a minimum to a maxi-mum value, or it might diverge in both directions from a zero pointin the middle of a range, or the values may wrap around in a cycle.Also, attributes may have hierarchical structure.32 2. What: Data Abstraction
Attributes
Attribute Types
Ordering DirectionCategorical Ordered
Ordinal Quantitative
Sequential Diverging Cyclic
Figure 2.7. Attribute types are categorical, ordinal, or quantitative. The direction
of attribute ordering can be sequential, diverging, or cyclic.
2.5.1 Categorical
The ﬁrst distinction is between categorical and ordered data. The
type of categorical data, such as favorite fruit or names, does not
have an implicit ordering, but it often has hierarchical structure.⋆⋆A synonym for categori-
calisnominal . Categories can only distinguish whether two things are the same(apples) or different (apples versus oranges). Of course, any ar-bitrary external ordering can be imposed upon categorical data.Fruit could be ordered alphabetically according to its name, orby its price—but only if that auxiliary information were available.However, these orderings are not implicit in the attribute itself, theway they are with quantitative or ordered data. Other examples ofcategorical attributes are movie genres, ﬁle types, and city names.
2.5.2 Ordered: Ordinal and Quantitative
Allordered data does have an implicit ordering, as opposed to un-
ordered categorical data. This type can be further subdivided. With
ordinal data, such as shirt size, we cannot do full-ﬂedged arith-
metic, but there is a well-deﬁned ordering. For example, largeminus medium is not a meaningful concept, but we know thatmedium falls between small and large. Rankings are another kind2.5. Attribute T ypes 33
of ordinal data; some examples of ordered data are top-ten lists of
movies or initial lineups for sports tournaments depending on pastperformance.
A subset of ordered data is quantitative data, namely, a mea-
surement of magnitude that supports arithmetic comparison. Forexample, the quantity of 68 inches minus 42 inches is a mean-ingful concept, and the answer of 26 inches can be calculated.Other examples of quantitative data are height, weight, tempera-ture, stock price, number of calling functions in a program, and
number of drinks sold at a coffee shop in a day. Both integers andreal numbers are quantitative data.
3
In this book, the ordered type is used often; the ordinal type is
only occasionally mentioned, when the distinction between it andthe quantitative type matters.
2.5.2.1 Sequential versus Diverging
Ordered data can be either sequential , where there is a homoge-
neous range from a minimum to a maximum value, or diverging ,
which can be deconstructed into two sequences pointing in oppo-site directions that meet at a common zero point. For instance,a mountain height dataset is sequential, when measured from a
minimum point of sea level to a maximum point of Mount Everest.Abathymetric dataset is also sequential, with sea level on one end
and the lowest point on the ocean ﬂoor at the other. A full elevation
dataset would be diverging, where the values go up for mountainson land and down for undersea valleys, with the zero value of sealevel being the common point joining the two sequential datasets.
2.5.2.2 Cyclic
Ordered data may be cyclic , where the values wrap around back
to a starting point rather than continuing to increase indeﬁnitely.Many kinds of time measurements are cyclic, including the hourof the day, the day of the week, and the month of the year.
2.5.3 Hierarchical Attributes
There may be hierarchical structure within an attribute or betweenmultiple attributes. The daily stock prices of companies collected
3In some domains the quantitative category is further split into interval versus
ratio data [Stevens 46]; this distinction is typically not useful when designing a
visual encoding, so in this book these types remain collapsed together into this
single category.34 2. What: Data Abstraction
over the course of a decade is an example of a time-series data-
set, where one of the attributes is time. In this case, time can beaggregated hierarchically, from individual days up to weeks, up tomonths, up to years. There may be interesting patterns at mul-tiple temporal scales, such as very strong weekly variations forweekday versus weekend, or more subtle yearly patterns show-ing seasonal variations in summer versus winter. Many kinds ofattributes might have this sort of hierarchical structure: for exam-ple, the geographic attribute of a postal code can be aggregated upto the level of cities or states or entire countries.
/trianglerightsldSection 13.4 covers hi-
erarchical aggregation in
more detail, and Section 7.5
covers the visual encoding
of attribute hierarchies.
2.6 Semantics
Knowing the type of an attribute does not tell us about its seman-
tics, because these two questions are crosscutting: one does notdictate the other. Different approaches to considering the seman-tics of attributes that have been proposed across the many ﬁeldswhere these semantics are studied. The classiﬁcation in this bookis heavily focused on the semantics of keys versus values, and therelated questions of spatial and continuous data versus nonspa-tial and discrete data, to match up with the idiom design choiceanalysis framework. One additional consideration is whether anattribute is temporal.
2.6.1 Key versus Value Semantics
Akey attribute acts as an index that is used to look up value at-
tributes.⋆The distinction between key and value attributes is im-⋆A synonym for key at-
tribute isindependent at-
tribute . A synonym for
value attribute isdepen-
dent attribute . The lan-
guage of independent and
dependent is common instatistics. In the languageof data warehouses, a syn-onym for independent isdi-
mension , and a synonym
fordependent ismeasure .portant for the dataset types of tables and ﬁelds, as shown in Fig-
ure 2.8.
2.6.1.1 Flat T ables
A simple ﬂat table has only one key, where each item corresponds
to a row in the table, and any number of value attributes. In thiscase, the key might be completely implicit, where it’s simply the in-dex of the row. It might be explicit, where it is contained within the
table as an attribute. In this case, there must not be any duplicatevalues within that attribute. In tables, keys may be categorical orordinal attributes, but quantititive attributes are typically unsuit-able as keys because there is nothing to prevent them from havingthe same values for multiple items.2.6. Semantics 35
Tables
Attributes (columns)
Items 
(rows)
Cell containing value
Multidimensional Table
Value in cellFields (Continuous)
Attributes (columns)
Value in cellCellGrid of positions
Figure 2.8. Key and value semantics for tables and ﬁelds.
For example, in Table 2.1, Name is a categorical attribute that
might appear to be a reasonable key at ﬁrst, but the last line shows
that two people have the same name, so it is not a good choice. Fa-
vorite Fruit is clearly not a key, despite being categorical, because
Pear appears in two different rows. The quantitative attribute of
Age has many duplicate values, as does the ordinal attribute of
Shirt Size . The ﬁrst attribute in this ﬂat table has an explicit unique
identiﬁer that acts as the key.4This key attribute could either be
ordinal, for example if the order that the rows were entered intothe table captures interesting temporal information, or categorical,if it’s simply treated as a unique code.
Figure 2.9 shows the order table from Figure 2.5 where each
attribute is colored according to its type. There is no explicit key:even the Order ID attribute has duplicates, because orders consist
of multiple items with different container sizes, so it does not actas a unique identiﬁer. This table is an example of using an implicitkey that is the row number within the table.
4It’s common to store the key attribute in the ﬁrst column, for understandability
by people and ease of building data structures by computers.36 2. What: Data Abstraction
22
1 = Quantitative
2 = Nominal3 = Ordinal
1 = Quantitat i
v
e
222 = Nominal
333= O
r
dinal quantitative
 ordinal categorical
Figure 2.9. The order table with the attribute columns colored by their type; none
of them is a key.
2.6.1.2 Multidimensional T ables
The more complex case is a multidimensional table , where multi-
ple keys are required to look up an item. The combination of all
keys must be unique for each item, even though an individual keyattribute may contain duplicates. For example, a common multidi-mensional table from the biology domain has a gene as one key and
time as another key, so that the value in each cell is the activity
level of a gene at a particular time.
The information about which attributes are keys and which are
values may not be available; in many instances determining which
attributes are independent keys versus dependent values is thegoal of the vis process, rather than its starting point. In this case,the successful outcome of analysis using vis might be to recast aﬂat table into a more semantically meaningful multidimensionaltable.2.6. Semantics 37
2.6.1.3 Fields
Although ﬁelds differ from tables a fundamental way because they
represent continuous rather than discrete data, keys and valuesare still central concerns. (Different vocabulary for the same basicidea is more common with spatial ﬁeld data, where the term in-
dependent variable is used instead of key , and dependent variable
instead of value .)
Fields are structured by sampling in a systematic way so that
each grid cell is spanned by a unique range from a continuousdomain. In spatial ﬁelds, spatial position acts as a quantitativekey, in contrast to a nonspatial attribute in the case of a table thatis categorical or ordinal. The crucial difference between ﬁelds andtables is that useful answers for attribute values are returned forlocations throughout the sampled range, not just the exact pointswhere data was recorded.
Fields are typically characterized in terms of the number of keys
versus values. Their multivariate structure depends on the number
of value attributes, and their multidimensional structure depends
on the number of keys. The standard multidimensional cases are2D and 3D ﬁelds for static measurements taken in two or threespatial dimensions,
5and ﬁelds with three or four keys, in the case
where these measurements are time-varying. A ﬁeld can be bothmultidimensional and multivariate if it has multiple keys and mul-tiple values. The standard classiﬁcation according to multivariatestructure is that a scalar ﬁeld has one attribute per cell, a vector
ﬁeld has two or more attributes per cell, and a tensor ﬁeld has
many attributes per cell.
⋆⋆ These deﬁnitions of
scalar ,vector , and ten-
sor follow the common
usage in vis. In a strict
mathematical sense, thesedistinctions are not techni-cally correct, since scalarsand vectors are included
as a degenerate case
of tensors. Mapping themathematical usage to thevis usage, scalars mean
mathematical tensors oforder 0, vectors mean
mathematical tensors oforder 1, and tensors mean
mathematical tensors oforder 2 or more.2.6.1.4 Scalar Fields
Ascalar ﬁeld is univariate, with a single value attribute at each
point in space. One example of a 3D scalar ﬁeld is the time-varying
medical scan above; another is the temperature in a room at eachpoint in 3D space. The geometric intuition is that each point ina scalar ﬁeld has a single value. A point in space can have sev-eral different numbers associated with it; if there is no underlyingconnection between them then they are simply multiple separatescalar ﬁelds.
2.6.1.5 Vector Fields
Avector ﬁeld is multivariate, with a list of multiple attribute values
at each point. The geometric intuition is that each point in a vector
5It’s also possible for a spatial ﬁeld to have just one key.38 2. What: Data Abstraction
ﬁeld has a direction and magnitude, like an arrow that can point in
any direction and that can be any length. The length might meanthe speed of a motion or the strength of a force. A concrete exampleof a 3D vector ﬁeld is the velocity of air in the room at a speciﬁc timepoint, where there is a direction and speed for each item. The di-mensionality of the ﬁeld determines the number of components inthe direction vector; its length can be computed directly from thesecomponents, using the standard Euclidean distance formula. Thestandard cases are two, three, or four components, as above.
2.6.1.6 T ensor Fields
Atensor ﬁeld has an array of attributes at each point, representing
a more complex multivariate mathematical structure than the listof numbers in a vector. A physical example is stress, which in thecase of a 3D ﬁeld can be deﬁned by nine numbers that representforces acting in three orthogonal directions. The geometric intution
is that the full information at each point in a tensor ﬁeld cannot berepresented by just an arrow and would require a more complexshape such as an ellipsoid.
2.6.1.7 Field Semantics
This categorization of spatial ﬁelds requires knowledge of the at-tribute semantics and cannot be determined from type informa-tion alone. If you are given a ﬁeld with multiple measured valuesat each point and no further information, there is no sure way toknow its structure. For example, nine values could represent manythings: nine separate scalar ﬁelds, or a mix of multiple vector ﬁeldsand scalar ﬁelds, or a single tensor ﬁeld.
2.6.2 T emporal Semantics
Atemporal attribute is simply any kind of information that re-
lates to time. Data about time is complicated to handle becauseof the rich hierarchical structure that we use to reason about time,and the potential for periodic structure. The time hierarchy isdeeply multiscale: the scale of interest could range anywhere fromnanoseconds to hours to decades to millennia. Even the commonwords time and date are a way to partially specify the scale of tem-
poral interest. Temporal analysis tasks often involve ﬁnding or ver-ifying periodicity either at a predetermined scale or at some scalenot known in advance. Moreover, the temporal scales of interestdo not all ﬁt into a strict hierarchy; for instance, weeks do not ﬁt2.6. Semantics 39
cleanly into months. Thus, the generic vis problems of transforma-
tion and aggregation are often particularly complex when dealingwith temporal data. One important idea is that even though the/trianglerightsldSection 3.4.2.3 intro-
duces the problem of
data transformation. Sec-tion 13.4 discusses thequestion of aggregation indetail.
dataset semantics involves change over time, there are many ap-
proaches to visually encoding that data—and only one of them isto show it changing over time in the form of an animation.
/trianglerightsldVision versus memory is
discussed further in Sec-
tion 6.5.Temporal attributes can have either value or key semantics. Ex-
amples of temporal attributes with dependent value semantics are
a duration of elapsed time or the date on which a transaction oc-curred. In both spatial ﬁelds and abstract tables, time can be anindependent key. For example, a time-varying medical scan canhave the independent keys of x, y, z, t to cover spatial position and
time, with the dependent value attribute of density for each com-bination of four indices to look up position and time. A temporalkey attribute is usually considered to have a quantitative type, al-though it’s possible to consider it as ordinal data if the durationbetween events is not interesting.
2.6.2.1 Time-Varying Data
A dataset has time-varying semantics when time is one of the key
attributes, as opposed to when the temporal attribute is a valuerather than a key. As with other decisions about semantics, thequestion of whether time has key or value semantics requires ex-ternal knowledge about the nature of the dataset and cannot bemade purely from type information. An example of a dataset withtime-varying semantics is one created with a sensor network thattracks the location of each animal within a herd by taking newmeasurements every second. Each animal will have new locationdata at every time point, so the temporal attribute is an indepen-dent key and is likely to be a central aspect of understanding thedataset. In contrast, a horse-racing dataset covering a year’s worthof races could have temporal value attributes such as the race starttime and the duration of each horse’s run. These attributes do in-deed deal with temporal information, but the dataset is not time-varying.
A common case of temporal data occurs in a time-series dataset,
namely, an ordered sequence of time–value pairs. These datasetsare a special case of tables, where time is the key. These time-value pairs are often but not always spaced at uniform temporalintervals. Typical time-series analysis tasks involve ﬁnding trends,correlations, and variations at multiple time scales such as hourly,daily, weekly, and seasonal.40 2. What: Data Abstraction
The word dynamic is often used ambiguously to mean one of
two very different things. Some use it to mean a dataset has time-
varying semantics, in contrast to a dataset where time is not a key
attribute, as discussed here. Others use it to mean a dataset has
stream type, in contrast to an unchanging ﬁle that can be loaded
all at once. In this latter sense, items and attributes can be added/trianglerightsldThe dataset types of dy-
namic streams versus static
ﬁles are discussed in Sec-tion 2.4.6.
or deleted and their values may change during a running session
of a vis tool. I carefully distinguish between these two meaningshere.
2.7 Further Reading
The Big Picture The framework presented here was inspired in part
by the many taxonomies of data that have been previouslyproposed, including the synthesis chapter at the beginning ofan early collection of infovis readings [Card et al. 99], a tax-onomy that emphasizes the division between continuous anddiscrete data [Tory and M ¨oller 04a], and one that emphasizes
both data and tasks [Shneiderman 96].
Field Datasets Several books discuss the spatial ﬁeld dataset type
in far more detail, including two textbooks [Telea 07, Wardet al. 10], a voluminous handbook [Hansen and Johnson 05],and the vtk book [Schroeder et al. 06].
Attribute T ypes The attribute types of categorical, ordered, and quan-
titative were proposed in the seminal work on scales of mea-surement from the psychophysics literature [Stevens 46].Scales of measurement are also discussed extensively in thebook The Grammar of Graphics [Wilkinson 05] and are used
as the foundational axes of an inﬂuential vis design spacetaxonomy [Card and Mackinlay 97].
Key and Value Semantics The Polaris vis system, which has been com-
mercialized as Tableau, is built around the distinction be-tween key attributes (independent dimensions) and value at-tributes (dependent measures) [Stolte et al. 02].
T emporal Semantics A good resource for time-oriented data vis
is a recent book, Visualization of Time-Oriented Data [Aigner
et al. 11].This page intentionally left blankThis page intentionally left blankTrendsActions
Analyze
Search
QueryWhy?
All Data
Outliers Features
Attributes
One Many
Distribution Dependency Correlation Similarity
Network Data
Spatial Data
ShapeTopology
PathsExtremesConsume
Present Enjoy Discover
Produce
Annotate Record Derive
Identify Compare Summarizetag
Target known Target unknown
Location 
known
Location 
unknownLookup
LocateBrowseExploreTargets
Why?
How?What?
Figure 3.1. Why people are using vis in terms of actions and targets.Why: T ask AbstractionChapter 3
3.1 The Big Picture
Figure 3.1 breaks down into actions and targets the reasons why
a vis tool is being used. The highest-level actions are to use vis
to consume or produce information. The cases for consuming areto present, to discover, and to enjoy; discovery may involve gen-erating or verifying a hypothesis. At the middle level, search canbe classiﬁed according to whether the identity and location of tar-gets are known or not: both are known with lookup, the target isknown but its location is not for locate, the location is known butthe target is not for browse, and neither the target nor the locationare known for explore. At the low level, queries can have threescopes: identify one target, compare some targets, and summarizeall targets. Targets for all kinds of data are ﬁnding trends and out-liers. For one attribute, the target can be one value, the extremesof minimum and maximum values, or the distribution of all valuesacross the entire attribute. For multiple attributes, the target canbe dependencies, correlations, or similarities between them. Thetarget with network data can be topology in general or paths inparticular, and with spatial data the target can be shape.
3.2 Why Analyze T asks Abstractly?
This framework encourages you to consider tasks in abstract form,rather than the domain-speciﬁc way that users typically thinkabout them.
Transforming task descriptions from domain-speciﬁc language
into abstract form allows you to reason about similarities and dif-ferences between them. Otherwise, it’s hard to make useful com-parisons between domain situations, because if you don’t do thiskind of translation then everything just appears to be different.That apparent difference is misleading: there are a lot of similar-
4344 3. Why: T ask Abstraction
ities in what people want to do once you strip away the surface
language differences.
For example, an epidimiologist studying the spread of a new
strain of inﬂuenza might initially describe her task as “contrastthe prognosis of patients who were intubated in the ICU morethan one month after exposure to patients hospitalized within theﬁrst week”, while a biologist studying immune system responsemight use language such as “see if the results for the tissue sam-ples treated with LL-37 match up with the ones without the pep-tide”. Even if you know what all the specialized vocabulary means,it’s still hard to think about what these two descriptions have incommon because they’re using different words: “contrast” versus“match up”. If you transform these into descriptions using a con-sistent set of generic terms, then you can spot that these two tasksare just two instances of the same thing: “compare values betweentwo groups”.
The analysis framework has a small set of carefully chosen
words to describe why people are using vis, designed to help you
crisply and concisely distinguish between different goals. This sethas verbs describing actions , and nouns describing targets . It’s
possible that you might decide to use additional terms to com-pletely and precisely describe the user’s goals; if so, strive to trans-late domain-speciﬁc terms into words that are as generic as possi-ble.
The same vis tool might be usable for many different goals. It is
often useful to consider only one of the user’s goals at a time, in or-der to more easily consider the question of how a particular idiom
supports that goal. To describe complex activities, you can specifya chained sequence of tasks, where the output of one becomes theinput to the next.
Another important reason to analyze the task is to understand
whether and how to transform the user’s original data into differentforms by deriving new data. That is, the task abstraction can andshould guide the data abstraction.
3.3 Who: Designer or User
It’s sometimes useful to augment an analysis instance speciﬁca-tion by indicating who has a goal or makes a design choice: the
designer of the vis or the end user of the vis. Both cases are com-mon.3.4. Actions 45
Vis tools fall somewhere along a continuum from speciﬁc to gen-
eral. On the speciﬁc side, tools are narrow: the designer has built
many choices into the design of the tool itself in a way that the usercannot override. These tools are limited in the kinds of data andtasks that they can address, but their strength is that users are notfaced with an overwhelming array of design choices. On the gen-eral side, tools are ﬂexible and users have many choices to make.The breadth of choices is both a strength and a limitation: usershave a lot of power, but they also may make ineffective choices ifthey do not have a deep understanding of many vis design issues.
Specialized vis tools are designed for speciﬁc contexts with a
narrow range of data conﬁgurations, especially those createdthrough a problem-driven process. These specialized datasets areoften an interesting mix of complex combinations of and specialcases of the basic data types. They also are a mix of original andderived data. In contrast, general vis tools are designed to handle awide range of data in a ﬂexible way, for example, by accepting anydataset of a particular type as input: tables, or ﬁelds, or networks.
/trianglerightsldDataset types are cov-
ered in Section 2.4.
Some particularly broad tools handle multiple dataset types, for in-stance, supporting transformations between tables and networks.
3.4 Actions
Figure 3.2 shows three levels of actions that deﬁne user goals. The
high-level choices describe how the vis is being used to analyze ,
either to consume existing data or to also produce additional data.
The mid-level choices cover what kind of search is involved, in
terms of whether the target and location are known or not. Thelow-level choices pertain to the kind of query : does the user need
to identify one target, compare some targets, or summarize all ofthe targets? The choices at each of these three levels are indepen-dent from each other, and it’s usually useful to describe actions atall three of them.
3.4.1 Analyze
At the highest level, the framework distinguishes between two pos-sible goals of people who want to analyze data using a vis tool:
users might want only to consume existing information or also to
actively produce new information.
The most common use case for vis is for the user to consume
information that has already been generated as data stored in a46 3. Why: T ask Abstraction
Analyze
Search
QueryConsume
Present Enjoy Discover
Produce
Annotate Record Derive
Identify Compare Summarizetag
Target known Target unknown
Location 
known
Location 
unknownLookup
LocateBrowseExploreActions
Figure 3.2. Three levels of actions: analyze, search, and query.
format amenable to computation. The framework has three fur-
ther distinctions within that case: whether the goal is to presentsomething that the user already understands to a third party, orfor the user to discover something new or analyze information that3.4. Actions 47
is not already completely understood, or for users to enjoy a vis to
indulge their casual interests in a topic.
3.4.1.1 Discover
The discover goal refers to using vis to ﬁnd new knowledge that was
not previously known. Discovery may arise from the serendipitousobservation of unexpected phenomena, but investigation may be
motivated by existing theories, models, hypotheses, or hunches.This usage includes the goal of ﬁnding completely new things; thatis, the outcome is to generate a new hypothesis. It also includes
the goal of ﬁguring out whether a conjecture is true or false; thatis, to verify —or disconﬁrm—an existing hypothesis.
While vis for discovery is often associated with modes of sci-
entiﬁc inquiry, it is not restricted to domain situations that areformally considered branches of science. The discover goal is oftendiscussed as the classic motivation for sophisticated interactive id-ioms, because the vis designer doesn’t know in advance what theuser will need to see.
⋆The fundamental motivation of this analysis⋆This distinction between
the goals of presentation of
the known and discovery of
the unknown is very com-
mon in the vis literature, butother sources may use dif-ferent terms, such as ex-
plain versus explore . framework is to help you separate out the questions of why the vis
is being used from how the vis idiom is designed to achieve those
goals, so I will repeatedly emphasize that why doesn’t dictate how .
3.4.1.2 Present
The present goal refers to the use of vis for the succinct commu-
nication of information, for telling a story with data, or guiding
an audience through a series of cognitive operations. Presenta-tion using vis may take place within the context of decision mak-ing, planning, forecasting, and instructional processes. The crucialpoint about the present goal is that vis is being used by somebody
to communicate something speciﬁc and already understood to an
audience.
Presentation may involve collaborative or pedagogical contexts,
and the means by which a presentation is given may vary accord-
ing to the size of the audience, whether the presentation is live orprerecorded, and whether the audience is in the same place as thepresenter. One classic example of a present vis is static informa-
tion graphics, such as a diagram in a newspaper or an image ina blog. However, the present goal is not intrinsically limited to a
static visual encoding idiom; it’s very possible to pursue this goalwith dynamic vis idioms that include interaction and animation.Once again, the decision about why is separable from how the id-48 3. Why: T ask Abstraction
iom is designed: presentation can be supported through a wide
variety of idiom design choices.
A crucial aspect of presentation is that the knowledge commu-
nicated is already known to the presenter in advance. Sometimesthe presenter knows it before using vis at all and uses the vis onlyfor communication. In other cases, the knowledge arose from thepresenter’s previous use of vis with the goal of discovery, and it’s
useful to think about a chained sequence of tasks where the outputof a discover session becomes the input to a present session.
3.4.1.3 Enjoy
The enjoy goal refers to casual encounters with vis. In these con-
texts, the user is not driven by a previously pressing need to verifyor generate a hypothesis but by curiosity that might be both stim-ulated and satisﬁed by the vis. Casual encounters with vis forenjoyment can be ﬂeeting, such as when looking at an infographicwhile reading a blog post. However, users can become sufﬁcientlyengaged with an enjoyable vis tool that they use it intensively for amore extended period of time.
One aspect of this classiﬁcation that’s tricky is that the goals
of the eventual vis user might not be a match with the user goalsconjectured by the vis designer. For example, a vis tool may havebeen intended by the designer for the goal of discovery with a par-ticular audience, but it might be used for pure enjoyment by adifferent group of people. In the analyses presented in this bookI’ll assume that these goals are aligned, but in your own experienceas a designer you might need to consider how they might diverge.
Figure 3.3 shows the Name Voyager, which was created for ex-
pectant parents deciding what to name their new baby. When theuser types characters of a name, the vis shows data for the popu-larity of names in the United States since 1900 that start with thatsequence of characters. The tool uses the visual encoding idiomwhere each name has a stripe whose height corresponds to popu-larity at a given time. Currently popular names are brighter, andgender is encoded by color. The Name Voyager appealed to manypeople with no interest in having children, who analyzed many dif-ferent historical trends and posted extensively about their ﬁndingsin their personal blogs, motivated by their own enjoyment ratherthan a pressing need [Wattenberg 05].3.4. Actions 49
Figure 3.3. Name Voyager, a vis tool originally intended for parents focused deciding on what to name their expected
baby, ended up being used by many nonparents to analyze historical trends for their own enjoyment. Left: Names
starting with ‘O’ had a notable dip in popularity in the middle of the century. Right: Names starting with ‘LA T’ showa trend of the 1970s. After [Wattenberg 05, Figures 2 and 3], using http:/ /www.babynamewizard.com.
3.4.2 Produce
In contrast to using vis only for consuming existing information, in
the produce case the intent of the user is to generate new material.
Often the goal with produce is to produce output that is used im-
mediately, as input to a next instance. Sometimes the user intendsto use this new material for some other vis-related task later on,such as discovery or presentation. Sometimes the intended use ofthe new material is for some other purpose that does not requirevis, such as downstream analysis using nonvisual tools. There arethree kinds of produce goals: annotate ,record , and derive .
3.4.2.1 Annotate
The annotate goal refers to the addition of graphical or textual an-
notations associated with one or more preexisting visualization el-ements, typically as a manual action by the user. When an annota-tion is associated with data items, the annotation could be thoughtof as a new attribute for them. For example, the user could anno-
/trianglerightsldAttributes are covered in
Chapter 2.
tate all of the points within a cluster with a text label.
3.4.2.2 Record
The record goal saves or captures visualization elements as persis-
tent artifacts. These artifacts include screen shots, lists of book-50 3. Why: T ask Abstraction
Figure 3.4. Graphical history recorded during an analysis session with T ableau. From [Heer et al. 08, Figure 1].
marked elements or locations, parameter settings, interaction logs,
or annotations. The record choice saves a persistent artifact, in
contrast to the annotate , which attaches information temporarily
to existing elements; an annotation made by a user can subse-quently be recorded. One interesting example of a record goal is
to assemble a graphical history , in which the output of each task
includes a static snapshot of the view showing its current state,and these snapshots accumulate in a branching meta-visualizationshowing what occurred during the user’s entire session of usingthe vis tool. Figure 3.4 shows an example from the Tableau vistool [Heer et al. 08]. Recording and retaining artifacts such as theseare often desirable for maintaining a sense of analytical prove-nance, allowing users to revisit earlier states or parameter settings.
3.4.2.3 Derive
The derive goal is to produce new data elements based on existing
data elements. New attributes can be derived from informationcontained within existing ones, or data can be transformed fromone type into another. Deriving new data is a critical part of the visdesign process. The common case is that deriving new data is achoice made by vis designers, but this choice could also be drivenby a user of a vis tool.
When you are faced with a dataset, you should always consider
whether to simply use it as is, or to transform it to another form:you could create newly derived attributes from the original ones, oreven transform the dataset from the original type to another one.
There is a strong relationship between the form of the data—
the attribute and dataset types—and what kinds of vis idioms are3.4. Actions 51
effective at displaying it. The good news is that your hands are
not tied as a designer because you can transform the data into aform more useful for the task at hand. Don’t just draw what you’regiven; decide what the right thing to show is, create it with a seriesof transformations from the original dataset, and draw that!
The ability to derive new data is why the data abstraction used
in a vis tool is an active choice on the part of the designer, ratherthan simply being dictated by what the user provides. Changingthe dataset to another form by deriving new attributes and typesgreatly expands the design space of possible vis idioms that youcan use to display it. The ﬁnal data abstraction that you choosemight simply be the dataset in its original form, but more complexdata abstractions based on deriving new attributes and types arefrequently necessary if you’re designing a vis tool for a complex,real-world use case. Similarly, when you consider the design ofan existing vis system, understanding how the original designerchose to transform the given dataset should be a cornerstone ofyour analysis.
A dataset often needs to be transformed beyond its original state
in order to create a visual encoding that can solve the desired prob-lem. To do so, we can create derived attributes that extend the
dataset beyond the original set of attributes that it contains.
⋆⋆A synonym for derive is
transform . In some cases, the derived attribute encodes the same data as
the original, but with a change of type. For example, a datasetmight have an original attribute that is quantitative data: for in-stance, ﬂoating point numbers that represent temperature. Forsome tasks, like ﬁnding anomalies in local weather patterns, that
raw data might be used directly. For another task, like decidingwhether water is an appropriate temperature for a shower, thatquantitative attribute might be transformed into a new derived at-tribute that is ordered: hot, warm, or cold. In this transformation,most of the detail is aggregated away. In a third example, whenmaking toast, an even more lossy transformation into a binary cat-egorical attribute might sufﬁce: burned or not burned.
In other cases, creating the derived attribute requires access
to additional information. For a geographic example, a categoricalattribute of city name could be transformed into two derived quan-titative attributes containing the latitude and longitude of the city.This transformation could be accomplished through a lookup to aseparate, external database.
A new derived attribute may be created using arithmetic, log-
ical, or statistical operations ranging from simple to complex. Acommon simple operation is subtracting two quantitative attributes52 3. Why: T ask Abstraction
Original Dataexports
imports
(a)Derived Datatrade balance = exports −importstrade 
balance
(b)
Figure 3.5. Derived attributes can be directly visually encoded. (a) T wo original
data attributes are plotted, imports and exports. (b) The quantitative derived at-
tribute of trade balance, the difference between the two originals, can be plotteddirectly.
to create a new quantitative difference attribute, which can then be
directly visually encoded. Figure 3.5 shows an example of encod-ing two attributes directly, versus encoding the derived variable ofthe difference between them. For tasks that require understandingthis difference, Figure 3.5(b) is preferable because it encodes thedifference directly. The user can interpret the information by judg-ing position along a common frame. In contrast, in Figure 3.5(a)the user must judge the difference in heights between the two orig-inal curves at each step, a perceptual operation that is more difﬁ-cult and demanding. This operation is simple because it is local-ized to a pair of attribute values; a more complex operation wouldrequire global computations across all values for an attribute, suchas averaging for a single attribute or the correlation between two ofthem.
Datasets can be transformed into new ones of a different type,
just as new attributes can be derived from existing ones. Thefull process of creating derived data may involve multiple stagesof transformation.
For example, the VxInsight system transforms a table of ge-
nomics data into a network through a multistage derivation pro-cess by ﬁrst creating a quantitative derived attribute of similarity,and then creating a derived network with links only between themost similar items [Davidson et al. 01]. The table had 6000 rowsof yeast genes, and 18 columns containing measurements of thegene activity level in a speciﬁc experimental condition. The valuesin the columns were used to derive a new attribute, the similar-3.4. Actions 53
ity score, deﬁned between each pair of genes. The similarity score
was computed using sophisticated statistical processing to be ro-bust in the presence of nonlinear and noisy data, as occurs in thissort of biological application. This derived attribute was then usedto create a derived network, where the nodes in the network weregenes. A link was established between two genes when the simi-larity score was high; speciﬁcally, links were created only for thetop 20 similarity scores.
3.4.3 Search
All of the high-level analyze cases require the user to search for
elements of interest within the vis as a mid-level goal.⋆The classi- ⋆The verb ﬁnd is often
used as a synonym in de-
scriptions of search tasks,
implying a successful out-come.ﬁcation of search into four alternatives is broken down according
to whether the identity and location of the search target is alreadyknown or not.
3.4.3.1 Lookup
If users already know both what they’re looking for and where itis, then the search type is simply lookup . For example, a user
of a tree vis showing the ancestral relationships between mammalspecies might want to look up humans, and can get to the rightspot quickly by remembering how humans are classiﬁed: they’rein the group that has live young rather than laying eggs like aplatypus or having a pouch like kangaroos, and within that grouphumans fall into the category of primates.
3.4.3.2 Locate
To ﬁnd a known target at an unknown location, the search type islocate : that is, ﬁnd out where the speciﬁc object is. In a similar
example, the same user might not know where to ﬁnd rabbits, andwould have to look around in a number of places before locatingthem as lagomorphs (not rodents)!
3.4.3.3 Browse
In contrast, the exact identity of a search target might not beknown in advance; rather, it might be speciﬁed based on char-acteristics. In this case, users are searching for one or more itemsthat ﬁt some kind of speciﬁcation, such as matching up with aparticular range of attribute values. When users don’t know ex-actly what they’re looking for, but they do have a location in mind54 3. Why: T ask Abstraction
of where to look for it, the search type is browse . For instance,
if a user of a tree vis is searching within a particular subtree for
leaf nodes having few siblings, it would be an instance of browse
because the location is known in advance, even though the exactidentity of the search target isn’t. Another example of browsing is auser of a vis tool with the visual encoding idiom of a line graph dis-playing the share price of multiple companies over the past month,who examines the share price of each line on June 15.
3.4.3.4 Explore
When users are not even sure of the location, the search type isexplore . It entails searching for characteristics without regard to
their location, often beginning from an overview of everything. Ex-amples include searching for outliers in a scatterplot, for anoma-
lous spikes or periodic patterns in a line graph of time-series data,or for unanticipated spatially dependent patterns in a choroplethmap.
3.4.4 Query
Once a target or set of targets for a search has been found, a low-level user goal is to query these targets at one of three scopes:
identify ,compare ,o r summarize . The progression of these three
corresponds to an increase in the amount of search targets underconsideration: one, some, or all. That is, identify refers to a single
target, compare refers to multiple targets, and summarize refers to
the full set of possible targets.
For a concrete example, consider different uses of a choropleth
map of US election results, where each state is color-coded by theparty that won. A user can identify the election results for one
state, compare the election results of one state to another, or sum-
marize the election results across all states to determine how many
favored one candidate or the other or to determine the overall dis-tribution of margin of victory values.
3.4.4.1 Identify
The scope of identify is a single target. If a search returns known
targets, either by lookup orlocate , then identify returns their char-
acteristics. For example, a user of a static map that representsUS election results by color coding each state red or blue, with thesaturation level of either hue showing the proportion, can identify3.5. T argets 55
the winning party and margin of victory for the state of California.
Conversely, if a search returns targets matching particular charac-teristics, either by browse orexplore , then identify returns speciﬁc
references. For instance, the election map user can identify the
state having the highest margin of victory.
3.4.4.2 Compare
The scope of compare is multiple targets. Comparison tasks are
typically more difﬁcult than identify tasks and require more so-phisticated idioms to support the user. For example, the capabilityof inspecting a single target in detail is often necessary, but notsufﬁcient, for comparison.
3.4.4.3 Summarize
The scope of summarize task is all possible targets. A synonym for
summarize isoverview , a term is frequently used in the vis liter-
ature both as a verb, where it means to provide a comprehensiveview of everything, and as a noun, where it means a summary dis-play of everything. The goal of providing an overview is extremelycommon in visualization./trianglerightsldSection 6.7 discusses the
question of how and when
to provide overviews.
3.5 T argets
Figure 3.6 shows four kinds of abstract targets. The actions dis-
cussed above refer to a target , meaning some aspect of the data
that is of interest to the user. Targets are nouns, whereas actionsare verbs. The idea of a target is explicit with search and queryactions. It is more implicit with the use actions, but still relevant:for example, the thing that the user presents or discovers.
Three high-level targets are very broadly relevant, for all kinds
of data: trends ,outliers , and features .A trend is a high-level char-
acterization of a pattern in the data.
⋆Simple examples of trends in-⋆Indeed, a synonym for
trend is simply pattern .
clude increases, decreases, peaks, troughs, and plateaus. Almostinevitably, some data doesn’t ﬁt well with that backdrop; those el-ements are the outliers .
⋆The exact deﬁnition of features is task⋆There are many other
synonyms for outliers , in-
cluding anomalies ,novel-
ties,deviants , and sur-
prises .dependent, meaning any particular structures of interest.
Attributes are speciﬁc properties that are visually encoded. The
/trianglerightsldAttributes are discussed
in detail in Chapter 2.lowest-level target for an attribute is to ﬁnd an individual value.Another frequent target of interest is to ﬁnd the extremes: theminimum or maximum value across the range. A very common56 3. Why: T ask Abstraction
TrendsAll Data
Outliers Features
Attributes
One Many
Distribution Dependency Correlation Similarity
Network Data
Spatial Data
ShapeTopology
PathsExtremesTargets
Figure 3.6. The goals of the user might be to ﬁnd or understand speciﬁc aspects
of the data: trends and outliers for all kinds of data; individual values, the minimum
or maximum extremes of the range, or the entire distribution of a single attribute; orthe dependencies, correlations, or similarities between multiple attributes; topologyor paths for network data, and shape for spatial data.3.6. How: A Preview 57
target that has high-level scope is the distribution of all values for
an attribute.
Some targets encompass the scope of multiple attributes: de-
pendencies ,correlations , and similarities between attributes. A ﬁrst
attribute can have a dependency on a second, where the values for
the ﬁrst directly depend on those of the second. There is a correla-
tion between one attribute and another if there is a tendency for the
values of second to be tied to those of the ﬁrst. The similarity be-
tween two attributes can be deﬁned as a quantitative measurementcalculated on all of their values, allowing attributes to be rankedwith respect to how similar, or different, they are from each other.
The abstract tasks of understanding trends, outliers, distribu-
tions, and correlations are extremely common reasons to use vis.Each of them can be expressed in very diverse terms using domain-speciﬁc language, but you should be on the lookout to recognizethese abstractions.
Some targets pertain to speciﬁc types of datasets. Network data
speciﬁes relationships between nodes as links. The fundamentaltarget with network data is to understand the structure of theseinterconnections; that is, the network’s topology . A more speciﬁc
topological target is a path of one or more links that connects two
nodes. For spatial data, understanding and comparing the geo-
/trianglerightsldThe network datatype is
covered in Section 2.4.2,
and choices for how ar-range networks are coveredin Chapter 9.
metric shape is the common target of user actions.
/trianglerightsldSection 2.4.3.1 covers
the dataset type of spa-tial ﬁelds, and Section 2.4.4covers geometry. Choicesfor arranging spatial dataare covered in Chapter 8.3.6 How: A Preview
The third part of an analysis instance trio is how a vis idiom can
be constructed out of a set of design choices. Figure 3.7 provides
a preview of these choices, with a high-level breakdown into fourmajor classes.
The family of how to encode data within a view has ﬁve choices
for how to arrange data spatially: express values; separate, order,and align regions; and use given spatial data. This family also in-cludes how to map data with all of the nonspatial visual channelsincluding color, size, angle, shape, and many more. The manipu-late family has the choices of change any aspect of the view, selectelements from within the view, and navigate to change the view-
point within the view—an aspect of change with a rich enough setof choices to merit its own category. The family of how to facetdata between views has choices for how to juxtapose and coordi-nate multiple views, how to partition data between views, and howto superimpose layers on top of each other. The family of how to58 3. Why: T ask Abstraction
How?
Encode Manipulate Facet Reduce
Arrange
MapChange
Select
NavigateExpress Separate
Order Align
UseJuxtapose
Partition
SuperimposeFilter
AggregateEmbed
Color
MotionSize, Angle, Curvature, ...Hue Saturation Luminance
Shape
Direction, Rate, Frequency, ...from categorical and ordered 
attributes
Why?
How?
 What?
Figure 3.7. How to design vis idioms: encode, manipulate, facet, and reduce.
reduce the data shown has the options of ﬁlter data away, aggre-gate many data elements together, and embed focus and contextinformation together within a single view.
The rest of this book deﬁnes, describes, and discusses these
choices in depth.3.7. Analyzing and Deriving: Examples 59
3.7 Analyzing and Deriving: Examples
The three analysis and derivation examples below give a taste of
how this what–why–how framework can be used right away. Theﬁrst example covers comparative analysis between two vis tools.The second example discusses deriving a single attribute, an im-portance measure for trees to decide which branches to show tosummarize its topological structure. The third example covers de-riving many new attributes and augmenting a spatial ﬂuid dynam-ics dataset by creating derived spaces in which features of interestare easy to ﬁnd.
3.7.1 Comparing T wo Idioms
The what–why–how analysis framework is useful for comparativeanalysis, for example, to examine two different vis tools that havedifferent answers for the question of how the idiom is designed
when used for exactly the same context of why and what at the
abstraction level.
SpaceTree [Plaisant et al. 02], shown in Figure 3.8(a), and Tree-
Juxtaposer [Munzner et al. 03], shown in Figure 3.8(b), are tree vis
(a)
 (b)
Figure 3.8. Comparing two idioms. (a) SpaceT ree [Plaisant et al. 02]. (b) T reeJuxtaposer. From http:/ /www.cs.umd.
edu/hcil/spacetree and [Munzner et al. 03, Figure 1].60 3. Why: T ask Abstraction
Present Locate Identify
Path between two nodesActions
TargetsSpaceTree
TreeJuxtaposerEncode Navigate Select Filter AggregateTree
ArrangeWhy? What? How?
Encode Navigate Select
Figure 3.9. Analyzing what–why–how comparatively for the SpaceT ree and T reeJuxtaposer idioms.
tools that use somewhat different idioms. What these tools take as
input data is the same: a large tree composed of nodes and links.Why these tools are being used is for the same goal in this sce-nario: to present a path traced between two nodes of interest to acolleague. In more detail, both tools can be used to locate pathsbetween nodes and identify them.
Some aspects of idioms are the same: both systems allow the
user to navigate and to select a path, with the result that it’s en-coded differently from the nonselected paths through highlighting.The systems differ in how elements of the visualization are ma-nipulated and arranged. SpaceTree ties the act of selection to achange of what is shown by automatically aggregating and ﬁlteringthe unselected items. In contrast, TreeJuxtaposer allows the userto arrange areas of the tree to ensure visibility for areas of interest.Figure 3.9 summarizes this what–why–how analyis.
3.7.2 Deriving One Attribute
In a vis showing a complex network or tree, it is useful to be able toﬁlter out most of the complexity by drawing a simpler picture thatcommunicates the key aspects of its topological structure. Oneway to support this kind of summarization is to calculate a newderived attribute that measures the importance of each node inthe graph and ﬁlter based on that attribute. Many different ap-proaches to calculating importance have been proposed; centrality
metrics do so in a way that takes into account network topology.
The Strahler number is a measure of node importance originally3.7. Analyzing and Deriving: Examples 61
(a)
 (b)
Figure 3.10. The derived quantitative attribute of Strahler numbers is used to ﬁlter
the tree in order to create a recognizable summary. (a) The important skeleton of
a large tree is visible when only 5000 of the highest-ranked nodes are drawn. (b)The full tree has over a half million nodes. From [Auber 02, Figures 10 and 13].
developed in hydrogeology to characterize the branching structure
of rivers that has been adapted and extended for use visualizingtrees and networks [Auber 02]. Very central nodes have largeStrahler numbers, whereas peripheral nodes have low values. TheStrahler number is an example of a derived attribute for networkdata that is the result of a complex and global computation, ratherthan simply a local calculation on a small neighborhood around anode.
Figure 3.10 shows an example of ﬁltering according to the Strah-
ler derived attribute to summarize a tree effectively. The result ofdrawing only the top-ranked 5000 nodes and the links that con-nect them is a recognizable skeleton of the full tree, shown inFigure 3.10(a), while over a half million nodes are shown in Fig-ure 3.10(b). In contrast, if the 5000 nodes to draw were picked ran-domly, the structure would not be understandable. Both versionsof the network are also colored according to the Strahler number,to show how the centrality measure varies within the network.
To summarize this example concisely in terms of a what–why–
how analysis, as shown in Figure 3.11, a new quantitative attributeis derived and used to ﬁlter away the peripheral parts of a tree, insupport of the task of summarizing the tree’s overall topology. As inthe previous example, the tree is encoded as a node–link diagram,the most common choice for tree and network arrangment.62 3. Why: T ask Abstraction
Task 1
.58
.54
.64.84
.24.74
.64
.84
.84
.94.74
Out
Quantitative 
attribute on nodes.58
.54
.64.84
.24.74
.64
.84
.84
.94.74
In
Quantitative 
attribute on nodesTask 2
DeriveWhy? What?
In Tree Reduce SummarizeHow? Why? What?
In Quantitative attribute on nodes TopologyIn Tree
FilterIn
TreeOutFiltered tree
Removed 
unimportant partsInTree
+
Out  Quantitative 
attribute on nodes Out  Filtered tree
Figure 3.11. Analyzing a chained sequence of two instances where an attribute is derived in order to summarize a
tree by ﬁltering away the unimportant parts.
3.7.3 Deriving Many New Attributes
Data transformations can shed light into spatial data as well. In an
example from computational ﬂuid dynamics, linked derived spacesare used for feature detection [Henze 98]. The vis system shownin Figure 3.12 allows the user to quickly create plots of any twooriginal or derived variables from the palette of variables shownin the upper left derived ﬁelds pane. The views are linked together
with color highlighting. The power of this idiom lies in seeing whereregions that are contiguous in one view fall in the other views.
/trianglerightsldMultiple views are dis-
cussed further in Chap-
ter 12.
The original dataset is a time-varying spatial ﬁeld with measure-
ments along a curvilinear mesh ﬁtted to an airfoil. The plot in the
physical space pane on the upper right of Figure 3.12 shows the
data in this physical space, using the two spatial ﬁeld variables.Undisturbed airﬂow enters the physical space from the left, andthe back tip of the airfoil is on the right. Two important regionsin back of the airfoil are distinguished with color: a red recircula-tion region and a yellow wake region. While these regions are noteasy to distinguish in this physical view, they can be understood
and selected more easily by interaction with the four other derivedviews. For example, in the derived space of vorticity vs enthalpy in
the upper middle of Figure 3.12, the recirculation zone is distin-guishable as a coherent spatial structure at the top, with the yellowwake also distinguishable beneath it. As the white box shows, the3.7. Analyzing and Deriving: Examples 63
Figure 3.12. Computational ﬂuid dynamics vis showing the list of many derived attributes (top left), one view of
the original spatial ﬁeld (top right), and four other views showing pairs of selected derived attributes. The multiple
juxtaposed views are coordinated with shared colored highlights. From [Henze 98, Figure 5].
recirculation zone can easily be selected in this view. The pressure
vs temperature pane in the bottom middle of Figure 3.12 shows an-
other derived space made by plotting the pressure versus the tem-
perature. In this view, the red recirculation zone and the yellowwake appear where both the pressure and temperature variables
are high, in the upper right. Without getting into the exact tech-nical meaning of the derived variables as used in ﬂuid dynamics(vorticity, entropy, enthalpy, and so on), the point of this exampleis that many structures of interest in ﬂuid dynamics can be seenmore easily from layouts in the derived spaces.64 3. Why: T ask Abstraction
Task 1
Out
Many quantitative 
attributesIn
Many quantitative 
attributesTask 2
DeriveWhy? What?
In Spatial fieldHow? Why? What?
In Many quantitative 
attributes
FeaturesIn Spatial fieldInSpatial fieldOutJuxtaposed attribute plots with 
linked coloringIn
Spatial field
Actions
TargetsDiscover
Explore
Browse
Identify
CompareFacet ManipulateMap Arrange
Express Hue
Juxtapose
PartitionSelect
NavigateOut Many 
quantitative 
attributesOut  Juxtaposed 
attribute plots with linked coloring+
Figure 3.13. Analyzing a chained sequence, where many attributes are derived and visually encoded.
To summarize this example in terms of a what–why–how analy-
sis, as shown in Figure 3.13, many new quantitative attributes are
derived from an original spatial ﬁeld dataset. Each pair of themis visually encoded into a view, as is the original spatial data, andthe multiple juxtaposed views are coordinated with shared colorcoding and highlighting.
3.8 Further Reading
The Big Picture An earlier version of the what–why–how framework
was ﬁrst presented as a paper [Brehmer and Munzner 13],which includes a very detailed discussion of its relationshipto the extensive previous work in classiﬁcations of tasks andinteraction idioms. That discussion covers 30 previous clas-siﬁcations and 20 relevant references, ranging from a charac-terization of the scientiﬁc data analysis process [Springmeyeret al. 92], to an inﬂuential low-level task classiﬁcation [Amaret al. 05], to a taxonomy of tasks for network datasets [Leeet al. 06], to a recent taxonomy of interaction dynamics [Heerand Shneiderman 12].3.8. Further Reading 65
Who: Designers versus Users Some of the challenges inherent in bridg-
ing the gaps between vis designers and users are discussed
in an inﬂuential paper [van Wijk 06].
Derive Many vis pipeline models discuss the idea of data trans-
formation as a critical early step [Card et al. 99, Chi andRiedl 98], and others also point out the need to transform be-tween different attribute types [Velleman and Wilkinson 93].A later taxonomy of vis explicitly discusses the idea that data
types can change as the result of the transformation [Toryand M ¨oller 04b].
Examples The analysis examples are SpaceTree [Plaisant et al. 02],
TreeJuxtaposer [Munzner et al. 03], Strahler numbers for treesimpliﬁcation [Auber 02], and linked derived spaces for fea-ture detection [Henze 98].Domain situation
Observe target users using existing tools
Visual encoding/interaction idiomJustify design with respect to alternatives
AlgorithmMeasure system time/memoryAnalyze computational complexity
Observe target users after deployment ( )
Measure adoptionAnalyze results qualitatively
Measure human time with lab experiment ( lab study )Data/task abstraction
Figure 4.1. The four nested levels of vis design have different threats to validity at each level, and validation
approaches should be chosen accordingly.Analysis: Four Levels for ValidationChapter 4
4.1 The Big Picture
Figure 4.1 shows four nested levels of design: domain situation,
task and data abstraction, visual encoding and interaction idiom,and algorithm. The task and data abstraction level addresses thewhy and what questions, and the idiom level addresses the ques-
tion of how . Each of these levels has different threats to validity, so
it’s a good idea to choose your validation method with these levelsin mind.
4.2 Why Validate?
Validation is important for the reasons discussed in Chapter 1: thevis design space is huge, and most designs are ineffective. In thatchapter, I also discuss the many reasons that validation is a trickyproblem that is difﬁcult to get right. It’s valuable to think abouthow you might validate your choices from the very beginning ofthe design process, rather than leaving these considerations forthe end as an afterthought.
This chapter introduces two more levels of design to consider,
one above the why–what abstraction level and one below the how
idiom level. While this book focuses on the two middle levels, con-sidering all four is helpful when thinking about how to validatewhether a given design has succeeded.
4.3 Four Levels of Design
Splitting the complex problem of vis design into four cascading lev-els provides an analysis framework that lets you address differentconcerns separately. Figure 4.2 shows these four levels.
6768 4. Analysis: Four Levels for Validation
Data/task abstraction
Visual encoding/interaction idiom
AlgorithmDomain situation
Figure 4.2. The four nested levels of vis design.
At the top is the situation level, where you consider the details
of a particular application domain for vis. Next is the what–why
abstraction level, where you map those domain-speciﬁc problems
and data into forms that are independent of the domain. The fol-lowing how level is the design of idioms that specify the approach
to visual encoding and interaction. Finally, the last level is thedesign of algorithms to instantiate those idioms computationally.
These levels are nested; the output from an upstream level above
is input to the downstream level below. A block is the outcome of
the design process at that level. The challenge of this nesting isthat choosing the wrong block at an upstream level inevitably cas-cades to all downstream levels. If you make a poor choice in theabstraction stage, then even perfect choices at the idiom and algo-rithm levels will not result in a vis system that solves the intendedproblem.
The value of separating these concerns into four levels is that
you can separately analyze the question of whether each level hasbeen addressed correctly, independently of whatever order designdecisions were made in the process of building the vis tool. Al-though I encourage you to consider these four levels separately foranalysis, in practice you wouldn’t ﬁnalize design decisions at onelevel before moving on to the next. Vis design is usually a highlyiterative reﬁnement process, where a better understanding of the4.3. Four Levels of Design 69
blocks at one level will feed back and forward into reﬁning the
blocks at the other levels. Thus, it is one of many examples of theprinciple of design as redesign [Green 89].
4.3.1 Domain Situation
Blocks at this top level describe a speciﬁc domain situation , which
encompasses a group of target users, their domain of interest, theirquestions, and their data. The term domain is frequently used in
the vis literature to mean a particular ﬁeld of interest of the targetusers of a vis tool, for example microbiology or high-energy physicsor e-commerce. Each domain usually has its own vocabulary fordescribing its data and problems, and there is usually some exist-ing workﬂow of how the data is used to solve their problems. Thegroup of target users might be as narrowly deﬁned as a handful
of people working at a speciﬁc company, or as broadly deﬁned asanybody who does scientiﬁc research.
One example of a situation block is a computational biologist
working in the ﬁeld of comparative genomics, using genomic se-quence data to ask questions about the genetic source of adaptiv-ity in a species [Meyer et al. 09]. While one kind of situation is aspeciﬁc set of users whose questions about their data arise fromtheir work, situations arise in other contexts. For example, an-other situation is members of the general public making medicaldecisions about their healthcare in the presence of uncertainty [Mi-callef et al. 12].
At this level, situation blocks are identiﬁed : the outcome of
the design process is an understanding that the designer reachesabout the needs of the user. The methods typically used by de-signers to identify domain situation blocks include interviews, ob-servations, or careful research about target users within a speciﬁcdomain.
Developing a clear understanding of the requirements of a par-
ticular target audience is a tricky problem for a designer.
⋆While ⋆Working closely with a
speciﬁc target audience to
iteratively reﬁne a designis called user-centered de-
sign orhuman-centered
design in the human–com-
puter interaction literature.it might seem obvious to you that it would be a good idea to un-
derstand requirements, it’s a common pitfall for designers to cutcorners by making assumptions rather than actually engaging withany target users.
In most cases users know they need to somehow view their data,
but they typically cannot directly articulate their analysis needs ina clear-cut way. Eliciting system requirements is not easy, evenwhen you have unfettered access to target users ﬂuent in the vo-cabulary of the domain and immersed in its workﬂow. Asking70 4. Analysis: Four Levels for Validation
users to simply introspect about their actions and needs is no-
toriously insufﬁcient: what users say they do when reﬂecting ontheir past behavior gives you an incomplete picture compared withwhat they actually do if you observe them.
The outcome of identifying a situation block is a detailed set of
questions asked about or actions carried out by the target users,about a possibly heterogeneous collection of data that’s also un-derstood in detail. Two of the questions that may have been askedby the computational biologist working in comparative genomics
working above were “What are the differences between individualnucleotides of feature pairs?” and “What is the density of coverageand where are the gaps across a chromosome?” [Meyer et al. 09].In contrast, a very general question such as “What is the geneticbasis of disease?” is not speciﬁc enough to be useful as input tothe next design level.
4.3.2 T ask and Data Abstraction
Design at the next level requires abstracting the speciﬁc domainquestions and data from the domain-speciﬁc form that they haveat the top level into a generic representation. Abstracting into thedomain-independent vocabulary allows you to realize how domainsituation blocks that are described using very different languagemight have similar reasons why the user needs the vis tool andwhat data it shows.
Questions from very different domain situations can map to the
same abstract vis tasks. Examples of abstract tasks include brows-ing, comparing, and summarizing. Task blocks are identiﬁed bythe designer as being suitable for a particular domain situationblock, just as the situation blocks themselves are identiﬁed at thelevel above.
/trianglerightsldChapter 3 covers abstract
tasks in detail.
Abstract data blocks, however, are designed . Selecting a data
block is a creative design step rather than simply an act of identiﬁ-cation. While in some cases you may decide to use the data in ex-actly the way that it was identiﬁed in the domain situation, you willoften choose to transform the original data from its upstream formto something quite different. The data abstraction level requiresyou to consider whether and how the same dataset provided by auser should be transformed into another form. Many vis idiomsare speciﬁc to a particular data type, such as a table of numberswhere the columns contain quantitative, ordered, or categoricaldata; a node–link graph or tree; or a ﬁeld of values at every pointin space. Your goal is to determine which data type would support4.3. Four Levels of Design 71
a visual representation of it that addresses the user’s problem. Al-
though sometimes the original form of the dataset is a good matchfor a visual encoding that solves the problem, often a transforma-tion to another data type provides a better solution./trianglerightsldChapter 2 covers ab-
stract data types, and Sec-
tion 3.4.2.3 discusses trans-forming and deriving data.
Explicitly considering the choices made in abstracting from
domain-speciﬁc to generic tasks and data can be very useful in the
vis design process. The unfortunate alternative is to do this ab-straction implicitly and without justiﬁcation. For example, manyearly web vis papers implicitly posited that solving the “lost in hy-perspace” problem should be done by showing the searcher a vi-sual representation of the topological structure of the web’s hyper-link connectivity graph. In fact, people do not need an internalmental representation of this extremely complex structure to ﬁnda page of interest. Thus, no matter how cleverly the informationwas visually encoded at the idiom design level, the resulting vistools all incurred additional cognitive load for the user rather thanreducing it.
4.3.3 Visual Encoding and Interaction Idiom
At the third level, you decide on the speciﬁc way to create andmanipulate the visual representation of the abstract data blockthat you chose at the previous level, guided by the abstract tasksthat you also identiﬁed at that level. I call each distinct possibleapproach an idiom . There are two major concerns at play with
idiom design. One set of design choices covers how to create a sin-gle picture of the data: the visual encoding idiom controls exactly
what users see. Another set of questions involves how to manip-ulate that representation dynamically: the interaction idiom con-
trols how users change what they see. For example, the Word Treesystem [Wattenberg and Viegas 08] shown in Figure 4.3 combinesthe visual encoding idiom of a hierarchical tree representation ofkeywords laid out horizontally, preserving information about thecontext of their use within the original text, and the interactionidiom of navigation based on keyword selection. While it’s oftenpossible to analyze encoding and interaction idioms as separabledecisions, in some cases these decisions are so intertwined thatit’s best to consider the outcome of these choices to be a singlecombined idiom.
Idiom blocks are designed: they are the outcome of decisions
that you make. The design space of static visual encoding idiomsis already enormous, and when you consider how to manipulatethem dynamically that space of possibilities is even bigger. The
/trianglerightsldChapters 7 through 14
feature a thorough look at
the design space of vis id-ioms.72 4. Analysis: Four Levels for Validation
Figure 4.3. Word T ree combines the visual encoding idiom of a hierarchical tree of keywords laid out horizontally
and the interaction idiom of navigation based on keyword selection. From [Wattenberg and Viegas 08, Figure 3].
nested model emphasizes identifying task abstractions and decid-
ing on data abstractions in the previous level exactly so that youcan use them to rule out many of the options as being a bad matchfor the goals of the users. You should make decisions about goodand bad matches based on understanding human abilities, espe-cially in terms of visual perception and memory./trianglerightsldChapters 5 and 6 cover
principles of human percep-
tion and memory that arerelevant for making idiom
design choices.
While it’s common for vis tools to provide multiple idioms that
users might choose between, some vis tools are designed to be very
narrow in scope, supporting only a few or even just a single idiom.
4.3.4 Algorithm
The innermost level involves all of the design choices involved increating an algorithm : a detailed procedure that allows a computer
to automatically carry out a desired goal. In this case, the goalis to efﬁciently handle the visual encoding and interaction idioms
that you chose in the previous level. Algorithm blocks are alsodesigned, rather than just identiﬁed.
You could design many different algorithms to instantiate the
same idiom. For example, one visual encoding idiom for creatingimages from a three-dimensional ﬁeld of measurements, such asscans created for medical purposes with magnetic resonance imag-4.4. Angles of Attack 73
ing, is direct volume rendering. Many different algorithms have
been proposed as ways to achieve the requirements of this idiom,including ray casting, splatting, and texture mapping. You mightdetermine that some of these are better than others according tomeasures such as the speed of the computation, how much com-puter memory is required, and whether the resulting image is anexact match with the speciﬁed visual encoding idiom or just anapproximation.
The nested model emphasizes separating algorithm design,
where your primary concerns are about computational issues, fromidiom design, where your primary concerns are about human per-ceptual issues.
Of course, there is an interplay between these levels. For ex-
ample, a design that requires something to change dynamicallywhen the user moves the mouse may not be feasible if computingthat would take minutes or hours instead of a fraction of a second.However, clever algorithm design could save the day if you comeup with a way to precompute data that supports a fast enoughresponse.
4.4 Angles of Attack
There are two common angles of attack for vis design: top down orbottom up. With problem-driven work, you start at the top domain
situation level and work your way down through abstraction, id-iom, and algorithm decisions. In technique-driven work, you work
at one of the bottom two levels, idiom or algorithm design, whereyour goal is to invent new idioms that better support existing ab-stractions, or new algorithms that better support existing idioms.
In problem-driven vis, you begin by grappling with the problems
of some real-world user and attempt to design a solution that helpsthem work more effectively. In this vis literature, this kind of workis often called a design study . Often the problem can be solved
using existing visual encoding and interaction idioms rather thandesigning new ones, and much of the challenge lies at the abstrac-tion level. However, sometimes the problem motivates the designof new idioms, if you decide that no existing ones will adequatelysolve the abstracted design problem.
Considering the four levels of nested model explicitly can help
you avoid the pitfall of skipping important steps in problem-drivenwork. Some designers skip over the domain situation level com-pletely, short-circuit the abstraction level by assuming that the74 4. Analysis: Four Levels for Validation
ﬁrst abstraction that comes to mind is the correct one, and jump
immediately into the third level of visual encoding and interactionidiom design. I argue against this approach; the abstraction stageis often the hardest to get right. A designer struggling to ﬁnd theright abstraction may end up realizing that the domain situationhas not yet been adequately characterized and jump back up towork at that level before returning to this one. As mentioned above,the design process for problem-driven work is almost never strictlylinear; it involves iterative reﬁnement at all of the levels.
In technique-driven work, your starting point is an idea for a
new visual encoding or interaction idiom, or a new algorithm. In
this style of work, you start directly at one of the two lower levelsand immediately focus design at that level. Considering the nestedmodel can help you articulate your assumptions at the level justabove your primary focus: either to articulate the abstraction re-quirements for your new idiom, or to articulate the idiom require-ments for your algorithm.
The analysis framework of this book is focused on the what–
why abstraction and how idiom levels and is intended to help you
work in either direction. For problem-driven work, it allows you towork downward when searching for existing idioms by analyzingwhat design choices are appropriate for task abstraction that youhave identiﬁed and data abstraction that you have chosen. Fortechnique-driven work, it allows you to work upward by classifyingyour proposed idiom within the framework of design choices, giv-ing you a clear framework in which to discuss its relationship withpreviously proposed idioms. Similarly, it is helpful to explicitly an-alyze a new algorithm with respect to the idioms that it supports.Although in some cases this analysis is very straightforward, itcan sometimes be tricky to untangle connections between algo-rithms and idioms. Can your new algorithm simply be switchedfor a previous one, providing a faster way to compute the samevisual encoding? Or does your new algorithm result in a visualencoding different enough to constitutes a new idiom that requiresjustiﬁcation to show it’s a good match for human capabilities andthe intended task?
4.5 Threats to Validity
Validating the effectiveness of a vis design is difﬁcult because thereare so many possible questions on the table. Considering the va-/trianglerightsldSection 1.12 presented
many questions to consider
when validating a vis design. lidity of your decisions at each level of the nested model separately4.6. Validation Approaches 75
Domain situation
You misunderstood their needs
You’re showing them the wrong thing
Visual encoding/interaction idiomThe way you show it doesn’t work
AlgorithmYour code is too slowData/task abstraction
Figure 4.4. The four nested levels of vis design have different threats to validity at
each level.
can help you ﬁnd your way through this thicket of questions aboutvalidating your decisions, in the same way that the levels also con-strain the decision-making process itself.
Each of the four levels has a different set of threats to valid-
ity: that is, different fundamental reasons why you might have
made the wrong choices.
⋆Figure 4.4 summarizes the four classes⋆ I have borrowed the
evocative phrase threats to
validity from the computer
security domain, by way of
the software engineering lit-
erature. I use the word
validation rather than eval-
uation to underscore the
idea that validation is re-quired for every level andextends beyond user stud-
ies and ethnographic obser-
vation to include complex-ity analysis and benchmarktimings. In software engi-neering, validation is about
whether you have built the
right product, and veriﬁca-
tion is about whether you
have built the product right.
Similarly, in the simulationcommunity, validation of
the scientiﬁc model with re-spect to real-world obser-vations is similarly consid-ered separately from veri-
ﬁcation of the implementa-
tion, and connotes a level
of rigor beyond the methodsdiscussed here. My use ofvalidation includes both of
these questions.of threats, where they means the target users and you means the
vis designer:
•Wrong problem: You misunderstood their needs.
•Wrong abstraction: You’re showing them the wrong thing.
•Wrong idiom: The way you show it doesn’t work.
•Wrong algorithm: Your code is too slow.
4.6 Validation Approaches
Different threats require very different approaches to validation.
Figure 4.5 shows a summary of the threats and validation ap-proaches possible at each level. The rest of this section explains76 4. Analysis: Four Levels for Validation
Threat       Wrong problem
Threat   Wrong task/data abstraction
Threat       Ineffective encoding/interaction idiom
Threat       Slow algorithmValidate   Observe and interview target users
Validate   Analyze computational complexity
Validate   Measure system time/memory
Validate   Observe adoption ratesValidate   Test on target users, collect anecdotal evidence of utility
Validate   Field study, document human usage of deployed systemValidate   Qualitative/quantitative result image analysis
Validate   Lab study, measure human time/errors for taskValidate   Justify encoding/interaction design
Implement system
 Test on any users, informal usability study
Figure 4.5. Threats and validation at each of the four levels. Many threats at the
outer levels require downstream validation, which cannot be carried out until the
inner levels within them are addressed, as shown by the red lines. Any singleproject would only address a subset of these levels, not all of them at once.
these ideas in more detail. I give only a brief outline of each vali-
dation method here; the Further Reading section at the end of thischapter has pointers to more thorough discussions of their use.
The analysis below distinguishes between immediate and down-
stream validation approaches. An important corollary of the model
having nested levels is that most kinds of validation for the outerlevels are not immediate because they require results from thedownstream levels nested within them. These downstream de-pendencies add to the difﬁculty of validation: a poor showing of
a test may misdirect attention upstream, when in fact the prob-lem results from a poor choice at the current level. For example, apoor visual encoding choice may cast doubt when testing a legiti-mate abstraction choice, or poor algorithm design may cast doubtwhen testing an interaction technique. Despite their difﬁculties,4.6. Validation Approaches 77
the downstream validations are necessary. The immediate vali-
dations only offer partial evidence of success; none of them aresufﬁcient to demonstrate that the threat to validity at that levelhas been addressed.
This model uses the language of immediate and downstream
in order to make the discussion of the issues at each level eas-ier to understand—but it is not always necessary to carry out thefull process of design and implementation at each level before do-ing any downstream validation. There are many rapid prototyp-
ing methodologies for accelerating this process by creating low-ﬁdelity stand-ins exactly so that downstream validation can oc-cur sooner. For example, paper prototypes and Wizard of Oz test-ing [Dow et al. 05] can be used to get feedback from target usersabout abstraction and encoding designs before diving into design-ing or implementing any algorithms.
4.6.1 Domain Validation
At the top level, when characterizing the domain situation, a visdesigner is asserting that particular problems of the target audi-ence would beneﬁt from vis tool support. The primary threat isthat the problem is mischaracterized: the target users do not infact have these problems. An immediate form of validation is tointerview and observe the target audience to verify the character-ization, as opposed to relying on assumptions or conjectures. Acommon approach for this case is a ﬁeld study , where the investi-
gator observes how people act in real-world settings, rather thanby bringing them into a laboratory setting. Field studies for do-main situation assessment often involve gathering qualitative datathrough semi-structured interviews. The method of contextual in-quiry [Holtzblatt and Jones 93], where the researcher observesusers working in their real-world context and interrupts to askquestions when clariﬁcation is needed, is typically better suitedfor vis designers than silent observation because of the complexcognitive tasks that are targeted.
One downstream form of validation is to report the rate at which
the tool has been adopted by the target audience. Of course, adop-tion rates do not tell the whole story: many well-designed tools failto be adopted, and some poorly designed tools win in the market-place. Nevertheless, the important aspect of this signal is that itreports what the target users do of their own accord, as opposed tothe approaches below where target users are implicitly or explicitlyasked to use a tool. In particular, a tool that is actually used by its78 4. Analysis: Four Levels for Validation
intended users has reached a different level of success than one
that has only been used by its designers.
4.6.2 Abstraction Validation
At the abstraction level, the threat is that the identiﬁed task ab-straction blocks and designed data abstraction blocks do not solvethe characterized problems of the target audience. The key aspectof validation against this threat is that the system must be testedby target users doing their own work, rather than doing an abstracttask speciﬁed by the designers of the vis system.
A common downstream form of validation is to have a member
of the target user community try the tool, in hopes of collectinganecdotal evidence that the tool is in fact useful. These anecdotesmay have the form of insights found or hypotheses conﬁrmed. Ofcourse, this observation cannot be made until after all three ofthe other levels have been fully addressed, after the algorithm de-signed at the innermost level is implemented. Although this formof validation is usually qualitative, some inﬂuential work towardquantifying insight has been done [Saraiya et al. 05]. As with thelevel above, it’s important to distinguish between a discovery madeby a target user and one that you’ve make yourself; the former is amore compelling argument for the utility of the vis tool.
A more rigorous validation approach for this level is to conduct
a ﬁeld study to observe and document how the target audienceuses the deployed system, again as part of their real-world work-ﬂow. The key difference between ﬁeld studies at this level andthose just described for assessing domain situations is that you’reobserving how their behavior changes after intervening with thedeployment of a vis tool, as opposed to documenting their existingwork practices.
4.6.3 Idiom Validation
At the visual encoding and interaction idiom level, the threat is thatthe chosen idioms are not effective at communicating the desiredabstraction to the person using the system. One immediate vali-dation approach is to carefully justify the design of the idiom withrespect to known perceptual and cognitive principles. Evaluation
/trianglerightsldPerceptual and cognitive
principles will be covered in
Chapters 5 and 6. methods such as heuristic evaluation [Zuk et al. 08] and expert
review [Tory and M ¨oller 05] are a way to systematically ensure that
no known guidelines are being violated by the design.4.6. Validation Approaches 79
A downstream approach to validate against this threat is to
carry out a lab study : a controlled experiment in a laboratory set-
ting.⋆This method is appropriate for teasing out the impact of spe- ⋆The term user study is
common in the vis litera-
ture, but it’s used ambigu-ously: sometimes it’s nar-rowly used to mean only alab study , whereas other
times it might also be ap-plied to a ﬁeld study . I use
it broadly, to mean both ofthese.ciﬁc idiom design choices by measuring human performance on
abstract tasks that were chosen by the study designers. Many ex-perimental designs include both quantitative and qualitative mea-surements. It’s extremely common to collect the objective mea-surements of the time spent and errors made by the study par-ticipants; subjective measurements such as their preferences are
also popular. Other kinds of quantitative data that are sometimesgathered include logging actions such as mouse moves and clicksby instrumenting the vis tool, or tracking the eye movements of theparticipants with external gear. Qualitative data gathering often in-cludes asking participants to reﬂect about their strategies throughquestionnaires. In this context, the expected variation in humanbehavior is small enough that it is feasible to design experimentswhere the number of participants is sufﬁcient to allow testing forstatistical signiﬁcance during the analysis process.
Another downstream validation approach is the presentation of
and qualitative discussion of results in the form of still images orvideo. This approach is downstream because it requires an im-plemented system to carry out the visual encoding and interactionspeciﬁcations designed at this level. This validation approach isstrongest when there is an explicit discussion pointing out the de-sirable properties in the results, rather than assuming that everyreader will make the desired inferences by unassisted inspectionof the images or video footage. These qualitative discussions of im-ages sometimes occur as usage scenarios, supporting an argumentthat the tool is useful for a particular task–dataset combination.
A third appropriate form of downstream validation is the quan-
titative measurement of result images created by the implementedsystem; these are often called quality metrics . For example, many
measurable layout metrics such as number of edge crossings andedge bends have been proposed to assess drawings of node–linknetworks. Some of these metrics have been empirically testedagainst human judgement, while others remains unproved con-jectures.
Informal usability studies do appear in Figure 4.5, but I specif-
ically refrain from calling them a validation method. As Andrewseloquently states: “Formative methods [including usability studies]lead to better and more usable systems, but neither offer valida-tion of an approach nor provide evidence of the superiority of anapproach for a particular context” [Andrews 08]. They are listed80 4. Analysis: Four Levels for Validation
at this level because it is a very good idea to do them upstream
of attempting a validating laboratory or ﬁeld study. If the systemis unusable, no useful conclusions about its utility can be drawnfrom a user study. I distinguish usability studies from informaltesting with users in the target domain, as described for the levelabove. Although the informal testing with target users describedat the level above may uncover usability problems, the goal is tocollect anecdotal evidence that the system meets its design goals.Such anecdotes are much less convincing when they come from arandom person rather than a member of the target audience. Incontrast, in an informal usability study, the person using the sys-tem does not need to be in the target audience; the only constraintis that the user is not the system designer.
4.6.4 Algorithm Validation
At the algorithm level, the primary threat is that the algorithm issuboptimal in terms of time or memory performance, either to atheoretical minimum or in comparison with previously proposedalgorithms. Obviously, poor time performance is a problem if theuser expects the system to respond in milliseconds but instead theoperation takes hours or days.
/trianglerightsldThe issue of matching
system latency to user ex-
pectations is discussed inmore detail in Section 6.8.
An immediate form of validation is to analyze the computational
complexity of the algorithm, using the standard approaches from
the computer science literature. While many designers analyze al-gorithm complexity in terms of the number of items in the dataset,in some cases it will be more appropriate to consider the numberof pixels in the display.
The downstream form of validation is to measure the wall-clock
time and memory performance of the implemented algorithm. Thistype of measurement is so common that it’s nearly mandatory forpapers claiming a contribution at the algorithm level. The primaryconsideration is typically scalability in terms of how dataset size af-fects algorithm speed. One of the trickier questions is to determinewhat data you should use to test the algorithm. Considerations in-clude matching up with standard benchmarks , which are used in
previous papers, and incorporating a sufﬁciently broad set of data.
Another threat is incorrectness at the algorithm level, where
the implementation does not meet the speciﬁcation from the idiomlevel above. The problem could come from poor algorithm design,or the implementation of the algorithm could have bugs like anycomputer program. Establishing the correctness of a computerprogram is a notoriously difﬁcult problem, whether through carefultesting or formal methods.4.7. Validation Examples 81
The threat of algorithm incorrectness is often addressed implic-
itly rather than explicitly within the vis literature. Presenting still
images or videos created by the implemented algorithm is one formof implicit validation against this threat, where the reader of a pa-per can directly see that the algorithm correctness objectives havebeen met. Explicit qualitative discussion of why these images showthat the algorithm is in fact correct is not as common.
4.6.5 Mismatches
A common problem in weak vis projects is a mismatch between thelevel at which the beneﬁt is claimed and the validation methodolo-gies chosen. For example, the beneﬁt of a new visual encodingidiom cannot be validated by wall-clock timings of the algorithm,which addresses a level downstream of the claim. Similarly, thethreat of a mischaracterized task cannot be addressed through aformal laboratory study, where the task carried out by the partic-ipants is dictated by the study designers, so again the validationmethod is at a different level than the threat against the claim. Thenested model explicitly separates the vis design problem into levelsin order to guide validation according to the unique threats at eachlevel.
However, it would be impossible for any single research paper to
address all four levels in detail, because of limitations on space andtime—such a paper would require hundreds of pages and might
take a decade to ﬁnish! Instead, any individual research paperwould use only a small subset of these validation methods, wherecareful consideration is made of which methods match the levelsof design where research contributions are being claimed.
4.7 Validation Examples
This section presents examples of several vis research papers, an-alyzed according to the levels of vis design that they target andthe methods used to validate their beneﬁts. These projects alsoprovide a preview of many approaches to vis that are discussed inmore detail later in the book.
4.7.1 Genealogical Graphs
McGufﬁn and Balakrishnan present a system for the visualizationof genealogical graphs [McGufﬁn and Balakrishnan 05]. They pro-82 4. Analysis: Four Levels for Validation
(a)
 (b)
Figure 4.6. Genealogical graphs. (a) Three layouts for the dual-tree: classical node–link top-to-bottom at the top,
classical left-to-right on the left, and the new indented outline algorithm on the right. (b) Widget for subtree collapsing
and expanding with ballistic drags. From [McGufﬁn and Balakrishnan 05, Figures 13 and 14].
pose multiple new visual encoding idioms, including one based on
the dual-tree , a subgraph formed by the union of two trees, as
shown in Figure 4.6(a). Their prototype features sophisticated in-teraction idioms, including automatic camera framing, animatedtransitions, and a new widget for ballistically dragging out sub-trees to arbitrary depths as shown in Figure 4.6(b).
This exemplary paper explicitly covers all four levels. The ﬁrst
domain situation level is handled concisely but clearly: their do-main is genealogy, and they brieﬂy discuss the needs of and cur-rent tools available for genealogical hobbyists. The paper particu-larly shines in the analysis at the second abstraction level. Theypoint out that the very term family tree is highly misleading, be-4.7. Validation Examples 83
Justify encoding/interaction design
Qualitative result image analysis
Test on target users, collect anecdotal evidence of utility
Figure 4.7. Genealogical graphs [McGufﬁn and Balakrishnan 05] validation levels.
cause the data type in fact is a more general graph with specialized
constraints on its structure. They discuss conditions for which thedata type is a true tree, a multitree, or a directed acyclic graph.They map the domain problem of recognizing nuclear family struc-ture into an abstract task of determining subgraph structure. Atthe third level of the model, they discuss the strengths and weak-nesses of several visual encoding idiom design choices, includingusing connection, containment, adjacency and alignment, and in-dentation. They present in passing two more specialized encoding
/trianglerightsldDesign choices for visual
encoding idioms for network
data are discussed in Chap-
ter 9.idioms, fractal node–link and containment for free trees, before
presenting in detail their main proposal for visual encoding. Theyalso carefully address interaction idiom design, which also fallsinto the third level of the model. At the fourth level of algorithmdesign, they concisely cover the algorithmic details of dual-tree lay-out.
Three validation methods are used in this paper, shown in Fig-
ure 4.7. There is the immediate justiﬁcation of encoding and in-teraction idiom design decisions in terms of established principles,and the downstream method of a qualitative discussion of resultimages and videos. At the abstraction level, there is the down-stream informal testing of a system prototype with a target user tocollect anecdotal evidence.
4.7.2 MatrixExplorer
Henry and Fekete present the MatrixExplorer system for social net-work analysis [Henry and Fekete 06], shown in Figure 4.8. Its de-sign comes from requirements formalized by interviews and partic-84 4. Analysis: Four Levels for Validation
Figure 4.8. MatrixExplorer features both node–link and matrix representations in an interface designed for sociolo-
gists and historians to explore social networks. From [Henry and Fekete 06, Figure 1].
ipatory design sessions with social science researchers. They use
both matrix representations to minimize clutter for large and densegraphs and the more intuitive node–link representations of graphsfor smaller networks./trianglerightsldThe strengths and weak-
nesses of matrix and node–
link representations of net-works are discussed in Sec-
tion 9.4.
All four levels of the model are addressed, with validation at
three of the levels, shown in Figure 4.9. At the domain situa-
tion level, there is explicit characterization of the social networkanalysis domain, which is validated with the qualitative techniquesof interviews and an exploratory study using participatory designmethods with social scientists and other researchers who use so-cial network data. At the abstraction level, the paper includes adetailed list of requirements of the target user needs discussed interms of abstract tasks and data. There is a thorough discussion ofthe primary encoding idiom design decision to use both node–linkand matrix views to show the data, and also of many secondaryencoding issues. There is also a discussion of both basic interac-tion idioms and more complex interaction via interactive reorderingand clustering. In both cases the authors use the immediate val-idation method of justifying these design decisions. There is alsoan extensive downstream validation of this level using qualitativediscussion of result images. At the algorithm level, the focus ison the reordering algorithm. Downstream benchmark timings arementioned very brieﬂy.4.7. Validation Examples 85
Justify encoding/interaction design
Measure system time/memory
Qualitative result image analysisObserve and interview target users
Figure 4.9. MatrixExplorer [Henry and Fekete 06] validation methods.
4.7.3 Flow Maps
Phan et al. propose a system for creating ﬂow maps that show the
movement of objects from one location to another, and demon-
strate it on network trafﬁc, census data, and trade data [Phanet al. 05]. Flow maps reduce visual clutter by merging edges, butmost previous instances were hand drawn. They present auto-matic techniques inspired by graph layout algorithms to minimizeedge crossings and distort node positions while maintaining rela-tive positions, as shown in Figure 4.10. Figure 4.10(a) shows mi-
/trianglerightsldThe visual encoding of
geographic data is dis-
cussed in Section 8.3.1. gration to California, while Figure 4.10(b) shows the top ten states
sending migrants to California and New York.
In their paper, Phan et al. focus on the innermost algorithm
design level, but the idiom and abstraction levels are also cov-ered. Their analysis of the useful characteristics of hand-drawnﬂow maps falls into the abstraction level. At the idiom level, theyhave a brief but explicit description of the goals of their layout al-gorithm, namely, intelligent distortion of positions to ensure thatthe separation distance between nodes is greater than the maxi-mum thickness of the ﬂow lines while maintaining left–right and
up–down ordering relationships. The domain situation level is ad-dressed more implicitly than explicitly: there is no actual discus-sion of who uses ﬂow maps and why. However, the analysis ofhand-drawn ﬂow maps could be construed as an implicit claim oflongstanding usage needs.86 4. Analysis: Four Levels for Validation
(a)
 (b)
Figure 4.10. Flow maps showing migration patterns from 1995 to 2000 US Census data. (a) Migration from Cali-
fornia. (b) The top ten states that sent migrants to California shown in green, and to New Y ork in blue. From [Phan
et al. 05, Figures 1c and 10].
Four validation methods were used in this paper, shown in Fig-
ure 4.11. At the algorithm level, there is an immediate complexity
analysis. There is also a brief downstream report of system timing,saying that all images were computed in a few seconds. There isalso a more involved downstream validation through the qualita-
Justify encoding/interaction design
Computation complexity analysis
Measure system time/memory
Qualitative result image analysis
Figure 4.11. Flow map [Phan et al. 05] validation methods.4.7. Validation Examples 87
(a)
 (b)
Figure 4.12. LiveRAC supports exploration of system management time-series data with a reorderable matrix and
semantic zooming. (a) The ﬁrst several dozen rows have been stretched out to show sparklines for the devices. (b)
The top three rows have been enlarged more, so the charts appear in full detail. From [McLachlan et al. 08, Figure 3].
tive discussion of result images generated by their system. In this
case, the intent was mainly to discuss algorithm correctness issuesat the innermost algorithm level, as opposed to addressing the vi-sual encoding idiom level. At the idiom level, the authors justifytheir three fundamental requirements as the outcome of analyzinghand-drawn diagrams: intelligent distortion of positions, mergingof edges that share destinations, and intelligent edge routing.
4.7.4 LiveRAC
McLachlan et al. present the LiveRAC system for exploring sys-tem management time-series data [McLachlan et al. 08]. LiveRACuses a reorderable matrix of charts with stretch and squish nav-igation combined with semantic zooming, so that the chart’s vi-sual representation adapts to the available space. Figure 4.12(a)
/trianglerightsldReorderable matrix align-
ments are covered in Sec-
tion 7.5.2, semantic zoom-ing is covered in Sec-tion 11.5.2, and stretch andsquish navigation is cov-ered in Section 14.5.shows a mix of small boxes showing only a single attribute encoded
with color and somewhat larger boxes showing concise line charts.The top three rows have been enlarged in Figure 4.12(b), providingenough room that the representation switches to detailed chartswith axes and labels. The paper reports on an informal longitudi-nal ﬁeld study of its deployment to operators of a large corporate88 4. Analysis: Four Levels for Validation
Justify encoding/interaction design
Qualitative result image analysisObserve and interview target users
Field study, document usage of deployed 
system
Figure 4.13. LiveRAC [McLachlan et al. 08] validation methods.
web hosting service. Four validation methods were used in thispaper, shown in Figure 4.13.
At the domain situation level, the paper explains the roles and
activities of system management professionals and their existingworkﬂow and tools. The validation approach was interviews withthe target audience. The phased design methodology, where man-agement approval was necessary for access to the true target users,led to a mix of immediate and downstream timing for this valida-
tion: many of these interviews occurred after a working prototypewas developed. This project is a good example of the iterative pro-cess alluded to in Section 4.3.
At the abstraction level, the choice of a collection of time-series
data for data type is discussed early in the paper. The rationaleis presented in the opposite manner from the discussion above:rather than justifying that time-series data is the correct choice for
the system management domain, the authors justify that this do-
main is an appropriate one for studying this data type. The paperalso contains a set of explicit design requirements, which includesabstract tasks like search, sort, and ﬁlter. The downstream vali-dation for the abstraction level is a longitudinal ﬁeld study of thesystem deployed to the target users, life cycle engineers for man-
aged hosting services inside a large corporation.
At the visual encoding and interaction level, there is an exten-
sive discussion of design choices, with immediate validation by jus-4.7. Validation Examples 89
tiﬁcation in terms of design principles and downstream validation
through a qualitative discussion of the results. Algorithms are notdiscussed.
4.7.5 LinLog
Noack’s LinLog paper introduces an energy model for graph draw-
ing designed to reveal clusters in the data, where clusters are de-ﬁned as a set of nodes with many internal edges and few edges tonodes outside the set [Noack 03]. Energy-based and force-directedmethods are related approaches to network layout and have beenheavily used in information visualization. Previous models strove
/trianglerightsldForce-directed placement
is discussed in Section 9.2.
to enforce a layout metric of uniform edge lengths, but Noackpoints out that creating visually distinguishable clusters requireslong edges between them. Figure 4.14(a) shows the success of thisapproach, in contrast to the indifferentiated blob created by a pre-viously proposed method shown in Figure 4.14(b).
Although a quick glance might lead to an assumption that this
graph drawing paper has a focus on algorithms, the primary con-tribution is in fact at the visual encoding idiom level. The two vali-dation methods used in the paper are qualitative and quantitativeresult image analysis, shown in Figure 4.15.
Noack clearly distinguishes between the two aspects of energy-
based methods for force-directed graph layout: the energy modelitself versus the algorithm that searches for a state with minimumtotal energy. In the vocabulary of my model, his LinLog energymodel is a visual encoding idiom. Requiring that the edges betweenclusters are longer than those within clusters is a visual encoding
(a)
 (b)
Figure 4.14. The LinLog energy model reveals clusters in node–link graphs. (a)
LinLog clearly shows clusters with spatial separation. (b) The popular Fructerman-
Reingold model for force-directed placement does not separate the clusters.From [Noack 03, Figure 1].90 4. Analysis: Four Levels for Validation
Qualitative/quantitative result image analysis
Figure 4.15. LinLog [Noack 03] validation methods.
using the visual channel of spatial position. One downstream val-
idation approach in this paper is a qualitative discussion of resultimages, which is appropriate for a contribution at the encodinglevel. This paper also contains a validation method not listed inthe model, because it is relatively rare in vis: mathematical proof.These proofs are about the optimality of the model results whenmeasured by quantitative metrics involving edge lengths and nodedistances. Thus, this model classiﬁes it in the quantitative imageanalysis category, another appropriate method to validate at theidiom level.
This paper does not in fact address the innermost algorithm
level. Noack explicitly leaves the problem of designing better energy-minimization algorithms as future work, using previously proposedalgorithms to showcase the results of his model. The domain situ-ation level is handled concisely but adequately by referencing pre-vious work about application domains with graph data where thereis a need to see clusters. For the abstraction level, although thepaper does not directly use the vocabulary of task and data ab-
straction , it clearly states that the abstract task is ﬁnding clusters
and that the data abstraction is a network.
4.7.6 Sizing the Horizon
Heer et al. compare line charts to the more space-efﬁcient horizon
graphs [Heer et al. 09], as Figure 4.16 shows. They identify tran- /trianglerightsldLine charts are discussed
in Section 9.2. sition points at which reducing the chart height results in signiﬁ-cantly differing drops in estimation accuracy across the comparedchart types, and they ﬁnd optimal positions in the speed–accuracytrade-off curve at which viewers performed quickly without atten-dant drops in accuracy. This paper features lab studies that aredesigned to validate (or invalidate) speciﬁc design choices at the4.8. Further Reading 91
Figure 4.16. Experiment 2 of Sizing the Horizon compared ﬁlled line charts, one-band horizon graphs, and two-
band horizon graphs of different sizes to ﬁnd transition points where reducing chart height results in major drops in
estimation accuracy across chart types. From [Heer et al. 09, Figure 7].
Lab study, measure human time/errors for task
Figure 4.17. Lab studies as a validation method.
visual encoding and interaction idiom level by measuring time and
error rates of people carrying out abstracted tasks, as shown inFigure 4.17.
4.8 Further Reading
The Big Picture I ﬁrst presented the four-level nested model of vis
design as a paper [Munzner 09a], with a discussion of blocksand guidelines between them in a follow-up paper [Meyer
et al. 13]; both of these contain many more references to pre-vious and related work. McGrath’s analysis of the strengthsand limitations of different experimental methods is well worthreading [McGrath 94], and it inﬂuenced my partition of vali-dation techniques according to levels.92 4. Analysis: Four Levels for Validation
Problem-Driven Work A good entry point for problem-driven vis work
is a detailed discussion of design study methodology, with a
nine-stage framework for conducting them and suggestionsfor how to avoid 32 pitfalls [Sedlmair et al. 12]. Anotherframework for problem-driven work is the MultidimensionalIn-depth Long-term Case studies (MILC) approach, which alsoadvocates working closely with domain users [Shneidermanand Plaisant 06].
Abstraction Level A recent paper argues that both data and task ab-
stractions are important points of departure for vis design-ers [Pretorius and van Wijk 09]. The problems at the abstrac-tion level fall into the realm of requirements elicitation andanalysis in software engineering; a good starting point for thatliterature is a recent book chapter [Maalej and Thurimella 13].
Algorithm Level There are several existing books with a heavy focus
on the algorithm level, including two textbooks [Telea 07,Ward et al. 10] and a large handbook [Hansen and John-son 05]. Other options are recent survey papers on a particu-lar topic, or speciﬁc research papers for very detailed discus-sion about a given algorithm. The larger issues of algorithmdesign are certainly not unique to vis; an excellent general ref-erence for algorithms is a popular textbook that also coverscomplexity analysis [Cormen et al. 90].
Human–Computer Interaction A comprehensive textbook is a good
starting point for the academic human–computer interactionliterature [Sharp et al. 07]. A very accessible book is a goodstarting point for the large literature aimed at practitioners[Kuniavsky 03].
Evaluation Methods A book chapter provides an excellent survey and
overview of evaluation and validation methods for vis, includ-ing an extensive discussion of qualitative methods [Carpen-dale 08]. Another discussion of evaluation challenges in-cludes a call for more repositories of data and tasks [Plais-ant 04]. A viewpoint article contains the thoughts of sev-
eral researchers on why, how, and when to do user stud-ies [Kosara et al. 03].
Field Studies For ﬁeld studies, contextual inquiry is a particularly
important method and is covered well in a book by one of itspioneers [Holtzblatt and Jones 93].4.8. Further Reading 93
Experiment Design For lab studies, my current favorite references
for experiment design and analysis are a cogent and acces-
sible recent monograph [Hornbaek 13], a remarkably wittybook [Field and Hole 03], and a new textbook with many ex-amples featuring visualization [Purchase 12].Magnitude Channels: Ordered Attributes Identity Channels: Categorical Attributes
Spatial region
Color hueMotionShapePosition on common scalePosition on unaligned scaleLength (1D size)Tilt/angleArea (2D size)Depth (3D position)Color luminanceColor saturationCurvatureVolume (3D size)Channels: Expressiveness Types and Effectiveness Ranks
Figure 5.1. The effectiveness of channels that modify the appearance of marks depends on matching the expres-
siveness of channels with the attributes being encoded.Marks and ChannelsChapter 5
5.1 The Big Picture
Marks are basic geometric elements that depict items or links, and
channels control their appearance. The effectiveness of a channelfor encoding data depends on its type: the channels that percep-tually convey magnitude information are a good match for ordereddata, and those that convey identity information with categoricaldata. Figure 5.1 summarizes the channel rankings.
5.2 Why Marks and Channels?
Learning to reason about marks and channels gives you the build-ing blocks for analyzing visual encodings. The core of the designspace of visual encodings can be described as an orthogonal combi-nation of two aspects: graphical elements called marks, and visualchannels to control their appearance. Even complex visual encod-ings can be broken down into components that can be analyzed interms of their marks and channel structure.
5.3 Deﬁning Marks and Channels
Amark is a basic graphical element in an image. Marks are geo-
metric primitive objects classiﬁed according to the number of spa-tial dimensions they require. Figure 5.2 shows examples: a zero-dimensional ( 0D) mark is a point, a one-dimensional ( 1D) mark
is a line, and a two-dimensional ( 2D) mark is an area. A three-
dimensional ( 3D) volume mark is possible, but they are not fre-
quently used.
9596 5. Marks and Channels
Points Lines Areas
Figure 5.2. Marks are geometric primitives.
A visual channel is a way to control the appearance of marks,
independent of the dimensionality of the geometric primitive.⋆Fig- ⋆ The term channel is
popular in the vis litera-
ture and is not meant toimply any particular theoryabout the underlying mech-
anisms of human visual per-
ception. There are many,many synonyms for visual
channel : nearly any com-
bination of visual ,graphical ,
perceptual ,retinal for the
ﬁrst word, and channel ,at-
tribute ,dimension ,variable ,
feature , and carrier for the
second word.ure 5.3 shows a few of the many visual channels that can encode
information as properties of a mark. Some pertain to spatial po-sition, including aligned planar position, unaligned planar posi-tion, depth (3D position), and spatial region. Others pertain tocolor, which has three distinct aspects: hue, saturation, and lu-minance. There are three size channels, one for each added di-mension: length is 1D size, area is 2D size, and volume is 3D size.The motion-oriented channels include the motion pattern, for in-stance, oscillating circles versus straight jumps, the direction ofmotion, and the velocity. Angle is also a channel, sometimes calledtilt. Curvature is also a visual channel. Shape is a complex phe-nomenon, but it is treated as a channel in this framework.
HorizontalPosition
Vertical BothColor
Shape Tilt
Size
Length Area Volume
Figure 5.3. Visual channels control the appearance of marks.5.3. Deﬁning Marks and Channels 97
(a) (b) (c) (d)
Figure 5.4. Using marks and channels. (a) Bar charts encode two attributes using
a line mark with the vertical spatial position channel for the quantitative attribute,
and the horizontal spatial position channel for the categorical attribute. (b) Scat-terplots encode two quantitative attributes using point marks and both vertical andhorizontal spatial position. (c) A third categorical attribute is encoded by addingcolor to the scatterplot. (d) Adding the visual channel of size encodes a fourthquantitative attribute as well.
Figure 5.4 shows a progression of chart types, with each show-
ing one more quantitative data attribute by using one more visual
channel. A single quantitative attribute can be encoded with ver-tical spatial position. Bar charts are a common example of thisencoding: the height of the bar conveys a quantitative value forthat attribute, as in Figure 5.4(a). Bar charts show two attributes,but only one is quantitative: the other is the categorical attributeused to spread out the bars along the axis (in this case, the hor-izontal axis). A second, independent quantitative attribute can beencoded by using the visual channel of horizontal spatial positionto directly encode information. It doesn’t make sense any more touse a line for the mark in this case, so the mark type needs to bea point. This visual encoding, shown in Figure 5.4(b), is a scatter-plot. You cannot continue to add more spatial position channelswhen creating drawings in two-dimensional space, but many visualchannels are nonspatial. An additional categorical data attributecan be encoded in a scatterplot format using the visual channel ofhue (one aspect of color), as in Figure 5.4(c). Figure 5.4(d) showsthe addition of a fourth quantitative attribute encoded with the vi-sual channel of size.
In these examples, each attribute is encoded with a single chan-
nel. Multiple channels can be combined to redundantly encode thesame attribute. The limitation of this approach is that more chan-nels are “used up” so that not as many attributes can be encodedin total, but the beneﬁt is that the attributes that are shown willbe very easily perceived.
The size and shape channels cannot be used on all types of
marks: the higher-dimensional mark types usually have built-in98 5. Marks and Channels
constraints that arise from the way that they are deﬁned. An
area mark has both dimensions of its size constrained intrinsi-cally as part of its shape, so area marks typically are not sizecoded or shape coded. For example, an area mark denoting a stateor province within a country on a geographic map already has acertain size, and thus attempting to size code the mark with anadditional attribute usually doesn’t make sense.
1Similarly, the
treemap visual encoding idiom shows the hierarchical structureof a tree using nested area marks; Figure 9.8 shows an example.The size of these marks is determined by an existing attribute thatwas used in construction of the treemap, as is their shape andposition. Changing the size of a mark according to an additionalattribute would destroy the meaning of the visual encoding.
A line mark that encodes a quantitative attribute using length in
one direction can be size coded in the other dimension by changingthe width of the line to make it fatter. However, it can’t be sizecoded in the ﬁrst direction to make it longer because its length isalready “taken” with the length coding and can’t be co-opted by asecond attribute. For example, the bars in Figure 5.4(a) can’t besize coded vertically. Thus, even though lines are often consideredto be inﬁnitely thin objects in mathematical contexts, line marksused in visual encoding do take up a nonzero amount of area. Theycan be made wider on an individual basis to encode an additionalattribute, or an entire set of bars can simply be made wider in auniform way to be more visible.
Point marks can indeed be size coded and shape coded because
their area is completely unconstrained. For instance, the circles ofvarying size in the Figure 5.4(d) scatterplot are point marks thathave been size coded, encoding information in terms of their area.An additional categorical attribute could be encoded by changingthe shape of the point as well, for example, to a cross or a triangleinstead of a circle. This meaning of the term point is different
than the mathematical context where it implies something that isinﬁnitely small in area and cannot have a shape. In the context ofvisual encoding, point marks intrinsically convey information onlyabout position and are exactly the vehicle for conveying additional
information through area and shape.
1The cartogram visual encoding idiom, where exactly this kind of size coding of
an additional attribute on a set of geographic regions is carried out, is an exception.
This idiom carefully alters the boundaries with a uniﬁed calculation that guarantees
that the borders remain contiguous while attempting to preserve each area’s shape
as much as possible.5.4. Using Marks and Channels 99
5.3.1 Channel T ypes
The human perceptual system has two fundamentally different
kinds of sensory modalities. The identity channels tell us infor-
mation about what something is or where it is. In contrast, the
magnitude channels tell us how much of something there is.⋆⋆ In the psychophysics
literature, the identity chan-
nels are called metathetic
orwhat–where , and the
magnitude channels are
called prothetic or how
much .For instance, we can tell what shape we see: a circle, a trian-
gle, or a cross. It does not make much sense to ask magnitudequestions for shape. Other what visual channels are shape, the
color channel of hue, and motion pattern. We can tell what spatial
region marks are within, and where the region is.
In contrast, we can ask about magnitudes with line length: how
much longer is this line than that line? And identity is not a pro-ductive question, since both objects are lines. Similarly, we canask luminance questions about how much darker one mark is thananother, or angle questions about how much space is between apair of lines, or size questions about how much bigger one markis than another. Many channels give us magnitude information,including the size channels of length, area, and volume; two of thethree color channels, namely, luminance and saturation; and tilt.
5.3.2 Mark T ypes
The discussion so far has been focused on table datasets, wherea mark always represents an item. For network datasets, a markmight represent either an item—also known as a node—or a link.Link marks represent a relationship between items. The two linkmark types are connection and containment. A connection mark
shows a pairwise relationship between two items, using a line. Acontainment mark shows hierarchical relationships using areas,
and to do so connection marks can be nested within each other atmultiple levels.
⋆While the visual representation of the area mark ⋆Synonyms for contain-
ment are enclosure and
nesting .might be with a line that depicts its boundary, containment is fun-damentally about the use of area. Links cannot be represented by
points, even though individual items can be. Figure 5.5 summa-rizes the possibilities.
5.4 Using Marks and Channels
All channels are not equal: the same data attribute encoded withtwo different visual channels will result in different information100 5. Marks and Channels
Marks as Items/Nodes
Marks as LinksPoints Lines Areas
Containment Connection
Figure 5.5. Marks can represent individual items, or links between them.
content in our heads after it has passed through the perceptual
and cognitive processing pathways of the human visual system.
The use of marks and channels in vis idiom design should be
guided by the principles of expressiveness and effectiveness. Theseideas can be combined to create a ranking of channels accordingto the type of data that is being visually encoded. If you haveidentiﬁed the most important attributes as part of developing yourtask and data abstraction, you can ensure that they are encodedwith the highest ranked channels.
5.4.1 Expressiveness and Effectiveness
Two principles guide the use of visual channels in visual encoding:expressiveness and effectiveness.
The expressiveness principle dictates that the visual encoding
should express all of, and only, the information in the dataset at-tributes. The most fundamental expression of this principle is thatordered data should be shown in a way that our perceptual systemintrinsically senses as ordered. Conversely, unordered data shouldnot be shown in a way that perceptually implies an ordering thatdoes not exist. Violating this principle is a common beginner’smistake in vis.
It’s no coincidence that the classiﬁcation of data attributes in
Chapter 2 has a central split along this very same line. This splitof channel types into two major categories is so fundamental tovisual encoding design that this distinction is built into the classi-5.4. Using Marks and Channels 101
ﬁcation at the ground level. The identity channels are the correct
match for the categorical attributes that have no intrinsic order.The magnitude channels are the correct match for the ordered at-tributes, both ordinal and quantitative.
The effectiveness principle dictates that the importance of the
attribute should match the salience of the channel; that is, its no-
ticeability. In other words, the most important attributes shouldbe encoded with the most effective channels in order to be most no-ticeable, and then decreasingly important attributes can be matchedwith less effective channels.
The rest of this chapter is devoted to the question of what the
word effectiveness means in the context of visual encoding.
5.4.2 Channel Rankings
Figure 5.6 presents effectiveness rankings for the visual channelsbroken down according to the two expressiveness types of orderedand categorical data. The rankings range from the most effectivechannels at the top to the least effective at the bottom.
Ordered attributes should be shown with the magnitude chan-
nels. The most effective is aligned spatial position , followed by un-
aligned spatial position . Next is length , which is one-dimensional
size, and then angle , and then area , which is two-dimensional size.
Position in 3D, namely, depth , is next. The next two channels are
roughly equally effective: luminance and saturation . The ﬁnal two/trianglerightsldLuminance and satura-
tion are aspects of color dis-
cussed in Chapter 10.
channels, curvature and volume (3D size), are also roughly equiva-
lent in terms of accuracy.
Categorical attributes should be shown with the identity chan-
nels. The most effective channel for categorical data is spatial re-
gion , with color hue as the next best one. The motion channel is /trianglerightsldHue is an aspect of color
discussed in Chapter 10. also effective, particularly for a single set of moving items against
a sea of static ones. The ﬁnal identity channel appropriate for cat-egorical attributes is shape .
While it is possible in theory to use a magnitude channel for
categorical data or a identity channel for ordered data, that choicewould be a poor one because the expressiveness principle wouldbe violated.
The two ranked lists of channels in Figure 5.6 both have chan-
nels related to spatial position at the top in the most effective spot.Aligned and unaligned spatial position are at the top of the list forordered data, and spatial region is at the top of the list for cate-gorical data. Moreover, the spatial channels are the only ones thatappear on both lists; none of the others are effective for both data102 5. Marks and Channels
Magnitude Channels: Ordered Attributes Identity Channels: Categorical Attributes
Spatial region
Color hueMotionShapePosition on common scalePosition on unaligned scaleLength (1D size)Tilt/angleArea (2D size)Depth (3D position)Color luminanceColor saturationCurvatureVolume (3D size)Channels: Expressiveness Types and Effectiveness Ranks
Figure 5.6. Channels ranked by effectiveness according to data and channel type. Ordered data should be shown
with the magnitude channels, and categorical data with the identity channels.
types. This primacy of spatial position applies only to 2D positions
in the plane; 3D depth is a much lower-ranked channel. These/trianglerightsldThe limitations and ben-
eﬁts of 3D are covered in
Section 6.3.fundamental observations have motivated many of the vis idioms
illustrated in this book, and underlie the framework of idiom designchoices. The choice of which attributes to encode with position isthe most central choice in visual encoding. The attributes encodedwith position will dominate the user’s mental model —their internal
mental representation used for thinking and reasoning—comparedwith those encoded with any other visual channel.
These rankings are my own synthesis of information drawn
from many sources, including several previous frameworks, exper-imental evidence from a large body of empirical studies, and my5.5. Channel Effectiveness 103
own analysis. The further reading section at the end of this chap-
ter contains pointers to the previous work. The following sectionsof this chapter discuss the reasons for these rankings at length.
5.5 Channel Effectiveness
To analyze the space of visual encoding possibilities you need tounderstand the characteristics of these visual channels, becausemany questions remain unanswered: How are these rankings jus-tiﬁed? Why did the designer decide to use those particular visual
channels? How many more visual channels are there? What kindsof information and how much information can each channel en-code? Why are some channels better than others? Can all ofthe channels be used independently or do they interfere with eachother?
This section addresses these questions by introducing the anal-
ysis of channels according to the criteria of accuracy, discrim-inability, separability, the ability to provide visual popout, and theability to provide perceptual groupings.
5.5.1 Accuracy
The obvious way to quantify effectiveness is accuracy : how close
is human perceptual judgement to some objective measurement ofthe stimulus? Some answers come to us from psychophysics , the
subﬁeld of psychology devoted to the systematic measurement ofgeneral human perception. We perceive different visual channelswith different levels of accuracy; they are not all equally distin-guishable. Our responses to the sensory experience of magnitudeare characterizable by power laws, where the exponent depends onthe exact sensory modality: most stimuli are magniﬁed or com-pressed, with few remaining unchanged.
Figure 5.7 shows the psychophysical power law of Stevens
[Stevens 75]. The apparent magnitude of all sensory channels fol-lows a power function based on the stimulus intensity:
S=I
n, (5.1)
where Sis the perceived sensation and Iis the physical inten-
sity. The power law exponent nranges from the sublinear 0.5 for
brightness to the superlinear 3.5 for electric current. That is, thesublinear phenomena are compressed, so doubling the physical104 5. Marks and Channels
Figure 5.7. Stevens showed that the apparent magnitude of all sensory channels
follows a power law S=In, where some sensations are perceptually magniﬁed
compared with their objective intensity (when n> 1) and some compressed (when
n< 1). Length perception is completely accurate, whereas area is compressed
and saturation is magniﬁed. Data from Stevens [Stevens 75, p. 15].
brightness results in a perception that is considerably less than
twice as bright. The superlinear phenomena are magniﬁed: dou-bling the amount of electric current applied to the ﬁngertips resultsis a sensation that is much more than twice as great. Figure 5.7shows that length has an exponent of n=1.0, so our perception of
length is a very close match to the true value. Here length means
the length of a line segment on a 2D plane perpendicular to the ob-server. The other visual channels are not perceived as accurately:area and brightness are compressed, while red–gray saturation ismagniﬁed.
Another set of answers to the question of accuracy comes from
controlled experiments that directly map human response to vi-sually encoded abstract information, giving us explicit rankings ofperceptual accuracy for each channel type. For example, Clevelandand McGill’s experiments on the magnitude channels [Clevelandand McGill 84a] showed that aligned position against a commonscale is most accurately perceived, followed by unaligned positionagainst an identical scale, followed by length, followed by angle.Area judgements are notably less accurate than all of these. Theyalso propose rankings for channels that they did not directly test:after area is an equivalence class of volume, curvature, and lumi-5.5. Channel Effectiveness 105
Positions
Rectangular 
areas 
(aligned or in a 
treemap)Angles
Circular 
areasCleveland & McGill’s  Results
Crowdsourced Results1.0 3.0 1.5 2.5 2.0
Log Error
1.0 3.0 1.5 2.5 2.0
Log Error
Figure 5.8. Error rates across visual channels, with recent crowdsourced results replicating and extending seminal
work from Cleveland and McGill [Cleveland and McGill 84a]. After [Heer and Bostock 10, Figure 4].
nance; that class is followed by hue in last place. (This last place
ranking is for hue as a magnitude channel, a very different matterthan its second-place rank as a identity channel.) These accuracyresults for visual encodings dovetail nicely with the psychophysicalchannel measurements in Figure 5.7. Heer and Bostock conﬁrmedand extended this work using crowdsourcing, summarized in Fig-ure 5.8 [Heer and Bostock 10]. The only discrepancy is that thelater work found length and angle judgements roughly equivalent.106 5. Marks and Channels
The rankings in Figure 5.6 are primarily based on accuracy,
which differs according to the type of the attribute that is being
encoded, but also take into account the other four considerations.
5.5.2 Discriminability
The question of discriminability is: if you encode data using a par-
ticular visual channel, are the differences between items percepti-ble to the human as intended? The characterization of visual chan-nel thus should quantify the number of bins that are available for
use within a visual channel, where each bin is a distinguishablestep or level from the other.
For instance, some channels have a very limited number of
bins. Consider line width: changing the line size only works fora fairly small number of steps. Increasing the width past that limitwill result in a mark that is perceived as a polygon area rather thana line mark. A small number of bins is not a problem if the numberof values to encode is also small. For example, Figure 5.9 shows anexample of effective linewidth use. Linewidth can work very well toshow three or four different values for a data attribute, but it wouldbe a poor choice for dozens or hundreds of values. The key factoris matching the ranges: the number of different values that needto be shown for the attribute being encoded must not be greaterthan the number of bins available for the visual channel used toencode it. If these do not match, then the vis designer should ei-ther explicitly aggregate the attribute into meaningful bins or usea different visual channel.
5.5.3 Separability
You cannot treat all visual channels as completely independentfrom each other, because some have dependencies and interactionswith others. You must consider a continuum of potential interac-tions between channels for each pair, ranging from the orthogonaland independent separable channels to the inextricably combined
integral channels. Visual encoding is straightforward with sepa-
rable channels, but attempts to encode different information inintegral channels will fail. People will not be able to access the de-
sired information about each attribute; instead, an unanticipatedcombination will be perceived.
Clearly, you cannot separately encode two attributes of informa-
tion using vertical and horizontal spatial position and then expectto encode a third attribute using planar proximity. In this case it5.5. Channel Effectiveness 107
Figure 5.9. Linewidth has a limited number of discriminable bins.
is obvious that the third channel precludes the use of the ﬁrst two.
However, some of the interchannel interference is less obvious.
Figure 5.10 shows pairs of visual channels at four points along
this continuum. On the left is a pair of channels that are com-pletely separable: position and hue. We can easily see that thepoints fall into two categories for spatial position, left and right.We can also separately attend to their hue and distinguish the redfrom the blue. It is easy to see that roughly half the points fall into
each of these categories for each of the two channels.
Next is an example of interference between channels, showing
that size is not fully separable from color hue. We can easily distin-
guish the large half from the small half, but within the small halfdiscriminating between the two colors is much more difﬁcult. Sizeinteracts with many visual channels, including shape.108 5. Marks and Channels
Position
    Hue (Color)Size    Hue (Color)Width    HeightRed    Green
Fully separable Some interference Some/significant 
interferenceMajor interference
Figure 5.10. Pairs of visual channels fall along a continuum from fully separable
to intrinsically integral. Color and location are separable channels well suited to
encode different data attributes for two different groupings that can be selectivelyattended to. However, size interacts with hue, which is harder to perceive for smallobjects. The horizontal size and and vertical size channels are automatically fused
into an integrated perception of area, yielding three groups. Attempts to code
separate information along the red and green axes of the RGB color space fail,because we simply perceive four different hues. After [Ware 13, Figure 5.23].
The third example shows an integral pair. Encoding one vari-
able with horizontal size and another with vertical size is ineffective
because what we directly perceive is the planar size of the circles,namely, their area. We cannot easily distinguish groupings of widefrom narrow, and short from tall. Rather, the most obvious per-ceptual grouping is into three sets: small, medium, and large. Themedium category includes the horizontally ﬂattened as well as thevertically ﬂattened.
The far right on Figure 5.10 shows the most inseparable chan-
nel pair, where the red and green channels of the RGB color spaceare used. These channels are not perceived separately, but inte-grated into a combined perception of color. While we can tell thatthere are four colors, even with intensive cognitive effort it is verydifﬁcult to try to recover the original information about high andlow values for each axis. The RGB color system used to specifyinformation to computers is a very different model than the colorprocessing systems of our perceptual system, so the three chan-nels are not perceptually separable.
/trianglerightsldColor is discussed in de-
tail in Section 10.2.
Integrality versus separability is not good or bad; the important
idea is to match the characteristics of the channels to the informa-tion that is encoded. If the goal is to show the user two differentdata attributes, either of which can be attended to selectively, thena separable channel pair of position and color hue is a good choice.If the goal is to show a single data attribute with three categories,5.5. Channel Effectiveness 109
then the integral channel pair of horizontal and vertical size is a
reasonable choice because it yields the three groups of small, ﬂat-tened, and large.
Finally, integrality and separability are two endpoints of a con-
tinuum, not strictly binary categories. As with all of the otherperceptual issues discussed in this chapter, many open questions
remain. I do not present a deﬁnitive list with a categorization foreach channel pair, but it’s wise to keep this consideration in mindas you design with channels.
5.5.4 Popout
Many visual channels provide visual popout , where a distinct item
stands out from many others immediately.⋆Figure 5.11 shows two ⋆ Visual popout is of-
ten called preattentive pro-
cessing ortunable detec-
tion .examples of popout: spotting a red object from a sea of blue ones,or spotting one circle from a sea of squares. The great value ofpopout is that the time it takes us to spot the different object doesnot depend on the number of distractor objects. Our low-levelvisual system does massively parallel processing on these visualchannels, without the need for the viewer to consciously directlyattention to items one by one. The time it takes for the red circleto pop out of the sea of blue ones is roughly equal when there are15 blue ones as in Figure 5.11(a) or 50 as in Figure 5.11(b).
Popout is not an all-or-nothing phenomenon. It depends on
both the channel itself and how different the target item is fromits surroundings. While the red circle pops out from the seas of15 and 50 red squares in Figures 5.11(c) and 5.11(d) at roughly
(a) (b) (c) (d) (e) (f)
Figure 5.11. Visual popout. (a) The red circle pops out from a small set of blue circles. (b) The red circle pops out
from a large set of blue circles just as quickly. (c) The red circle also pops out from a small set of square shapes,
although a bit slower than with color. (d) The red circle also pops out of a large set of red squares. (e) The red circledoes not take long to ﬁnd from a small set of mixed shapes and colors. (f) The red circle does not pop out from alarge set of red squares and blue circles, and it can only be found by searching one by one through all the objects.After http:/ /www.csc.ncsu.edu/faculty/healey/PP by Christopher G. Healey.110 5. Marks and Channels
(a) (b) (c)
(d)
 (e) (f)
Figure 5.12. Many channels support visual popout, including (a) tilt, (b) size,
(c) shape, (d) proximity, and (e) shadow direction. (f) However, parallel line pairs
do not pop out from a sea of slightly tilted distractor object pairs and can only be
detected through serial search. After http:/ /www.csc.ncsu.edu/faculty/healey/PP byChristopher G. Healey.
the same time, this popout effect is slower than with the color
difference versions in Figures 5.11(a) and 5.11(b). The differencebetween red and blue on the color hue channel is larger than thedifference in shape between ﬁlled-in circles and ﬁlled-in squares.
Although many different visual channels provide popout on their
own, they cannot simply be combined. A red circle does not pop outautomatically from a sea of objects that can be red or blue and cir-cles or squares: the speed of ﬁnding the red circle is much faster inFigures 5.11(e) with few distracting objects than in Figure 5.11(f)with many distractors. The red circle can only be detected withserial search : checking each item, one by one. The amount of time
it takes to ﬁnd the target depends linearly on the number of dis-tractor objects.
Most pairs of channels do not support popout, but a few pairs
do: one example is space and color, and another is motion andshape. Popout is deﬁnitely not possible with three or more chan-nels. As a general rule, vis designers should only count on usingpopout for a single channel at a time.5.5. Channel Effectiveness 111
Popout occurs for many channels, not just color hue and shape.
Figures 5.12(a) through 5.12(e) show several examples: tilt, size,
shape, proximity, and even shadow direction. Many other chan-nels support popout, including several different kinds of motionsuch as ﬂicker, motion direction, and motion velocity. All of themajor channels commonly used in visual encoding that are shownin Figure 5.6 do support popout individually, although not in com-bination with each other. However, a small number of potentialchannels do not support popout. Figure 5.12(f) shows that par-allelism is not preattentively detected; the exactly parallel pair oflines does not pop out from the slightly angled pairs but requiresserial search to detect.
5.5.5 Grouping
The effect of perceptual grouping can arises from either the useof link marks, as shown in Figure 5.5, or from the use of iden-tity channels to encode categorical attributes, as shown in Fig-ure 5.6.
Encoding link marks using areas of containment or lines of
connection conveys the information that the linked objects forma group with a very strong perceptual cue. Containment is thestrongest cue for grouping, with connection coming in second.
Another way to convey that items form a group is to encode cat-
egorical data appropriately with the identity channels. All of theitems that share the same level of the categorical attribute can beperceived as a group by simply directing attention to that level se-lectively. The perceptual grouping cue of the identity channels isnot as strong as the use of connection or containment marks, buta beneﬁt of this lightweight approach is that it does not add addi-tional clutter in the form of extra link marks. The third strongestgrouping approach is proximity ; that is, placing items within the
same spatial region. This perceptual grouping phenomenon is thereason that the top-ranked channel for encoding categorical datais spatial region. The ﬁnal grouping channel is similarity with the
other categorical channels of hue and motion, and also shape ifchosen carefully. Logically, proximity is like similarity for spatialposition; however, from a perceptual point of view the effect of thespatial channels is so much stronger than the effect of the othersthat it is is useful to consider them separately.
For example, the categorical attribute of animal type with the
three levels of cat,dog , and wombat can be encoded with the three
hue bins of red,green , and blue respectively. A user who chooses112 5. Marks and Channels
to attend to the blue hue will automatically see all of the wombats
as a perceptual group globally, across the entire scene.
The shape channel needs to be used with care: it is possible to
encode categorical data with shape in a way that does not auto-matically create perceptual groupings. For example, the shapes ofa forward ‘C’ and a backward ‘C’ do not automatically form globallyselectable groups, whereas the shapes of a circle versus a star do.Similarly, motion also needs to be used with care. Although a setof objects moving together against a background of static objects isa very salient cue, multiple levels of motion all happening at oncemay overwhelm the user’s capacity for selective attention.
5.6 Relative versus Absolute Judgements
The human perceptual system is fundamentally based on relativejudgements, not absolute ones; this principle is known as Weber’s
Law .
⋆For instance, the amount of length difference we can detect ⋆More formally, Weber’s
Law is typically stated as
the detectable difference in
stimulus intensity Ias a
ﬁxed percentage Kof the
object magnitude: δI/I =
K.is a percentage of the object’s length.
This principle holds true for all sensory modalities. The fact that
our senses work through relative rather than absolute judgements
has far-ranging implications. When considering questions suchas the accuracy and discriminability of our perceptions, we mustdistinguish between relative and absolute judgements. For exam-ple, when two objects are directly next to each other and aligned,we can make much more precise judgements than when they arenot aligned and when they are separated with many other objectsbetween them.
An example based on Weber’s Law illuminates why position
along a scale can be more accurately perceived than a pure lengthjudgement of position without a scale. The length judgement inFigure 5.13(a) is difﬁcult to make with unaligned and unframedbars. It is easier with framing, as in Figure 5.13(b), or alignment,as in Figure 5.13(c), so that the bars can be judged against a com-mon scale. When making a judgement without a common scale,the only information is the length of the bars themselves. Placinga common frame around the bars provides another way to estimatemagnitude: we can check the length of the unﬁlled bar. Bar B isonly about 15% longer than Bar A, approaching the range wherelength differences are difﬁcult to judge. But the unﬁlled part ofthe frame for Bar B is about 50% smaller than the one for Bar A,an easily discriminable difference. Aligning the bars achieves thesame effect without the use of a frame.5.6. Relative versus Absolute Judgements 113
AB
Unframed 
Unaligned
(a)Framed 
UnalignedAB
(b)AB
Unframed 
Aligned
(c)
Figure 5.13. Weber’s Law states that we judge based on relative, not absolute
differences. (a) The lengths of unframed, unaligned rectangles of slightly different
sizes are hard to compare. (b) Adding a frame allows us to compare the very dif-ferent sizes of the unﬁlled rectangles between the bar and frame tops. (c) Aligningthe bars also makes the judgement easy. Redrawn and extended after [Clevelandand McGill 84a, Figure 12].
Another example shows that our perception of color and lumi-
nance is completely contextual, based on the contrast with sur-
rounding colors. In Figure 5.14(a), the two labeled squares in acheckerboard appear to be quite different shades of gray. In Fig-ure 5.14(b), superimposing a solid gray mask that touches bothsquares shows that they are identical. Conversely, Figure 5.15
(a)
 (b)
Figure 5.14. Luminance perception is based on relative, not absolute, judgements.
(a) The two squares A and B appear quite different. (b) Superimposing a gray
mask on the image shows that they are in fact identical.114 5. Marks and Channels
(a)
 (b)
Figure 5.15. Color perception is also relative to surrounding colors and depends on context. (a) Both cubes have
tiles that appear to be red. (b) Masking the intervening context shows that the colors are very different: with yellow
apparent lighting, they are orange; with blue apparent lighting, they are purple.
shows two colorful cubes. In Figure 5.15(a) corresponding squares
both appear to be red. In Figure 5.15(b), masks show that thetile color in the image apparently illuminated by a yellowish lightsource is actually orange, and for the bluish light the tiles are actu-ally purple. Our visual system evolved to provide color constancy
so that the same surface is identiﬁable across a broad set of illumi-nation conditions, even though a physical light meter would yieldvery different readings. While the visual system works very wellin natural environments, many of its mechanisms work againstsimple approaches to visually encoding information with color.
5.7 Further Reading
The Big Picture The highly inﬂuential theory of visual marks and
channels was proposed by Bertin in the 1960s [Bertin 67].The ranking of channel effectiveness proposed in this chap-ter is my synthesis across the ideas of many previous authorsand does not come directly from any speciﬁc source. It was in-ﬂuenced by the foundational work on ranking of visual chan-nels through measured-response experiments [Cleveland andMcGill 84a], models [Cleveland 93a], design guidelines for5.7. Further Reading 115
matching visual channels to data type [Mackinlay 86], and
books on visualization [Ware 13] and cartography [MacEach-ren 95]. It was also affected by the more recent work oncrowdsourced judgements [Heer and Bostock 10], taxonomy-based glyph design [Maguire et al. 12], and glyph design ingeneral [Borgo et al. 13].
Psychophysical Measurement The foundational work on the variable
distinguishability of different visual channels, the categoriza-
tion of channels as metathetic identity and prothetic magni-tude, and scales of measurement was done by a pioneer inpsychophysics [Stevens 57, Stevens 75].
Effectiveness and Expressiveness Principles The principles of expres-
siveness for matching channel to data type and effectivenessfor choosing the channels by importance ordering appearedin a foundational paper [Mackinlay 86].
Perception This chapter touches on many perceptual and cognitive
phenomena, but I make no attempt to explain the mecha-nisms that underlie them. I have distilled an enormous liter-ature down to the bare minimum of what a beginning vis de-signer needs to get started. The rich literature on perceptionand cognitive phenomena is absolutely worth a closer look,because this chapter only scratches the surface; for example,the Gestalt principles are not covered.
Ware offers a broad, thorough, and highly recommended in-
troduction to perception for vis in his two books [Ware 08,Ware 13]. His discussion includes more details from nearlyall of the topics in this chapter, including separability andpopout. An overview of the literature on popout and otherperceptual phenomena appears on a very useful page that in-cludes interactive demos http:/ /www.csc.ncsu.edu/faculty/healey/PP [Healey 07]; one of the core papers in this litera-ture begins to untangle what low-level features are detectedin early visual processing [Treisman and Gormican 88].•No Unjustiﬁed 3D
–The Power of the Plane
–The Disparity of Depth
–Occlusion Hides Information
–Perspective Distortion Dangers
–Tilted T ext Isn’t Legible
•No Unjustiﬁed 2D
•Eyes Beat Memory
•Resolution over Immersion
•Overview First, Zoom and Filter, Detail on Demand
•Responsiveness Is Required
•Get It Right in Black and White
•Function First, Form Next
Figure 6.1. Eight rules of thumb.Rules of ThumbChapter 6
6.1 The Big Picture
This chapter contains rules of thumb : advice and guidelines. Each
of them has a catchy title in hopes that you’ll remember it as a
slogan. Figure 6.1 lists these eight rules of thumb.
6.2 Why and When to Follow Rules of Thumb?
These rules of thumb are my current attempt to synthesize the cur-rent state of knowledge into a more uniﬁed whole. In some cases Irefer to empirical studies, in others I make arguments based on myown experience, and some have been proposed in previous work.They are not set in stone; indeed, they are deeply incomplete. Thecharacterization of what idioms are appropriate for which task anddata abstractions is still an ongoing research frontier, and thereare many open questions.
6.3 No Unjustiﬁed 3D
Many people have the intuition that if two dimensions are good,three dimensions must be better—after all, we live in a three-dimensional world. However, there are many difﬁculties in visu-ally encoding information with the third spatial dimension, depth,which has important differences from the two planar dimensions.
In brief, 3D vis is easy to justify when the user’s task involves
shape understanding of inherently three-dimensional structures.In this case, which frequently occurs with inherently spatial data,the beneﬁts of 3D absolutely outweigh the costs, and designers canuse the many interaction idioms designed to mitigate those costs.
In all other contexts, the use of 3D needs to be carefully justi-
ﬁed. In most cases, rather than choosing a visual encoding using
117118 6. Rules of Thumb
three dimensions of spatial position, a better answer is to visually
encode using only two dimensions of spatial position. Often anappropriate 2D encoding follows from a different choice of data ab-straction, where the original dataset is transformed by computingderived data.
The cues that convey depth information to our visual system
include occlusion, perspective distortion, shadows and lighting,familiar size, stereoscopic disparity, and others. This section dis-cusses the costs of these depth cues in a visual encoding context
and the challenges of text legibility given current display technol-ogy. It then discusses situations where the beneﬁts of showingdepth information could outweigh these costs and the need for jus-tiﬁcation that the situation has been correctly analyzed.
6.3.1 The Power of the Plane
A crucial point when interpreting the channel rankings in Fig-ure 5.6 is that the spatial position channels apply only to planarspatial position, not arbitrary 3D position.
Vertical and horizontal position are combined into the shared
category of planar because the differences between the up–down
and side-to-side axes are relatively subtle. We do perceive heightdifferences along the up–down axis as more important than hor-izontal position differences, no doubt due to the physical effectsof gravity in real life. While the vertical spatial channel thus hasa slight priority over the horizontal one, the aspect ratio of stan-
dard displays gives more horizontal pixels than vertical ones, soinformation density considerations sometimes override this con-cern. For the perceived importance of items ordered within theaxes, reading conventions probably dominate. Most Western lan-guages go from left to right and from top to bottom, but Arabic andHebrew are read from right to left, and some Asian languages areread vertically.
6.3.2 The Disparity of Depth
The psychophysical power law exponents for accuracy shown inFigure 5.7 are different for depth position judgements in 3D thanfor planar position judgements in 2D. Our highly accurate lengthperception capability, with the linear nvalue of 1.0, only holds for
planar spatial position. For depth judgements of visual distance,nwas measured as 0.67 [Stevens 57]; that exponent is even worse
than the value of 0.7 for area judgements. This phenomenon is6.3. No Unjustiﬁed 3D 119
Toward AwayUp
DownRight
Left
(a)Thousands of points up/down and left/right
We can only see the outside shell of the world
(b)
Figure 6.2. Seeing planar position versus depth. (a) The sideways and up–down
axes are fundamentally different from the toward–away depth axis. (b) Along the
depth axis we can see only one point for each ray, as opposed to millions of raysfor the other two axes. After [Ware 08, page 44].
not surprising when considered mathematically, because as shown
in Figure 6.2 the length of a line that extends into the scene isscaled nonlinearly in depth, whereas a line that traverses the pic-ture plane horizontally or vertically is scaled linearly, so distancesand angles are distorted [St. John et al. 01].
Considered perceptually, the inaccuracy of depth judgements is
also not surprising; the common intuition that we experience theworld in 3D is misleading. We do not really live in 3D, or even 2.5D:to quote Colin Ware, we see in 2.05D [Ware 08]. That is, most of
the visual information that we have is about a two-dimensional im-
age plane , as deﬁned below, whereas the information that we have
about a third depth dimension is only a tiny additional fractionbeyond it. The number of 0.05is chosen somewhat arbitrarily to
represent this tiny fraction.
Consider what we see when we look out at the world along
a ray from some ﬁxed viewpoint, as in Figure 6.2(a). There isa major difference between the toward–away depth axis and theother two axes, sideways and up–down. There are millions of raysthat we can see along these two axes by simply moving our eyes,to get information about the nearest opaque object. This infor-mation is like a two-dimensional picture, often called the image
plane . In contrast, we can only get information at one point along
the depth axis for each ray away from us toward the world, asin Figure 6.2(b). This phenomenon is called line-of-sight ambigu-
ity[St. John et al. 01]. In order to get more information about what
is hidden behind the closest objects shown in the image plane, we120 6. Rules of Thumb
would need to move our viewpoint or the objects. At best we could
change the viewpoint by simply moving our head, but in manycases we would need to move our body to a very different position.
6.3.3 Occlusion Hides Information
The most powerful depth cue is occlusion , where some objects can-
not be seen because they are hidden behind others. The visibleobjects are interpreted as being closer than the occluded ones.The occlusion relationships between objects change as we movearound; this motion parallax allows us to build up an understand-
ing of the relative distances between objects in the world.
When people look at realistic scenes made from familiar objects,
the use of motion parallax typically does not impose cognitive loador require conscious attention. In synthetic scenes, navigationcontrols that allow the user to change the 3D viewpoint interac-tively invoke the same perceptual mechanisms to provide motionparallax. In sufﬁciently complex scenes where a single ﬁxed view-point does not provide enough information about scene structure,interactive navigation capability is critical for understanding 3Dstructure. In this case, the cost is time: interactive navigationtakes longer than inspecting a single image.
The overarching problem with occlusion in the context of visual
encoding is that presumably important information is hidden, anddiscovering it via navigation has a time cost. In realistic environ-ments, there is rarely a need to inspect all hidden surfaces. How-
ever, in a vis context, the occluded detail might be critical. It isespecially likely to be important when using spatial position as avisual channel for abstract, nonspatial data.
Moreover, if the objects have unpredictable and unfamiliar
shapes, understanding the three-dimensional structure of the scenecan be very challenging. In this case there can be appreciable cog-nitive load because people must use internal memory to rememberthe shape from previous viewpoints, and internally synthesize anunderstanding of the structure. This case is common when usingthe spatial position channels for visual encoding. Figure 6.3 illus-trates the challenges of understanding the topological structure ofa node–link graph laid out in 3D, as an example of the unfamiliarstructure that arises from visually encoding an abstract dataset.Synthesizing an understanding of the structure of the linkages hid-den from the starting viewpoint shown here is likely to take a con-siderable amount of time. While sophisticated interaction idiomshave been proposed to help users do this synthesis more quickly6.3. No Unjustiﬁed 3D 121
Figure 6.3. Resolving the 3D structure of the occluded parts of the scene is possi-
ble with interactive navigation, but that takes time and imposes cognitive load, even
when sophisticated interaction idioms are used, as in this example of a node–linkgraph laid out in 3D space. From [Carpendale et al. 96, Figure 21].
than with simple realistic navigation, thus lowering the time cost,
vis designers should always consider whether the beneﬁts of 3Dare worth the costs.
6.3.4 Perspective Distortion Dangers
The phenomenon of perspective distortion is that distant objects
appear smaller and change their planar position on the imageplane. Imagine a photograph looking along railroad tracks: al-/trianglerightsldThe disparity in our per-
ception of depth from our
perception of planar spa-
tial position is discussed in
Section 6.3.2.though they are of course parallel, they appear to draw together as
they recede into the distance. Although the tracks have the samewidth in reality, measuring with a ruler on the photograph itselfwould show that in the picture the width of the nearby track ismuch greater than that of the distant track.
⋆⋆The phenomenon of per-
spective distortion is also
known as foreshortening .One of the major breakthroughs of Western art was the Renais-
sance understanding of the mathematics of perspective to createvery realistic images, so many people think of perspective as a good122 6. Rules of Thumb
Figure 6.4. 3D bar charts are more difﬁcult than 2D bar charts because of both
perspective distortion and occlusion. From [Few 07, Question 7].
thing. However, in the context of visually encoding abstract data,
perspective is a very bad thing! Perspective distortion is one ofthe main dangers of depth because the power of the plane is lost;it completely interferes with visual encodings that use the planarspatial position channels and the size channel. For example, it ismore difﬁcult to judge bar heights in a 3D bar chart than in mul-tiple horizontally aligned 2D bar charts, as shown in Figure 6.4.Foreshortening makes direct comparison of bar heights difﬁcult.
Figure 6.5 shows another example where size coding in multiple
dimensions is used for bars that recede into the distance in 3D ona ground plane. The result of the perspective distortion is thatthe bar sizes cannot be directly compared as a simple perceptualoperation.
Figure 6.5. With perspective distortion, the power of the planar spatial position
channel is lost, as is the size channel. From [Mukherjea et al. 96, Figure 1].6.3. No Unjustiﬁed 3D 123
6.3.5 Other Depth Cues
In realistic scenes, one of the depth cues is the size of familiar
objects. We roughly know the size of a car, so when we see one ata distance we can estimate the size of a nearby unfamiliar object.If all objects in the scene are visually encoded representations of
abstract information, we do not have access to this strong depthcue.
The depth cues of shadows and surface shading also commu-
nicate depth and three-dimensional structure information. Castshadows are useful for resolving depth ambiguity because they al-low us to infer the height of an object with respect to a groundplane. Shading and self-shadowing show the three-dimensionalshape of an object. One problem with using these lighting-basedcues when visualizing abstract data is that they create visual clut-ter that distracts the viewer’s attention from the meaningful partsof the scene that represent information. Another problem is thatcast shadows, regions of self-shadowing, or highlights could bemistaken by the viewer for true marks that are the substrate forthe visual channels showing attribute information. Cast shad-ows could also cause problems by occluding true marks. The ﬁ-nal problem is that surface shading effects interfere with the colorchannels: highlights can change the hue or saturation, and shad-ows change the luminance.
Stereoscopic depth is a cue that comes from the disparities be-
tween two images made from two camera viewpoints slightly sepa-rated in space, just like our two eyes are. In contrast, all of the pre-vious discussion pertained to pictoral cues from a single camera.Although many people assume that stereo vision is the strongestdepth cue, it is in fact a relatively weak one compared with theothers listed above and contributes little for distant objects. Stereodepth cues are most useful for nearby objects that are at roughlythe same depth, providing guidance for manipulating things withinarm’s reach.
Stereo displays, which deliver a slightly different image for each
of our two eyes, do help people better resolve depth. Conveniently,they do not directly interfere with any of the main visual channels.Stereo displays do indeed improve the accuracy of depth perceptioncompared with single-view displays—but even still depth cannot beperceived with the accuracy of planar position. Of course, stereocannot solve any of the problems associated with perspective dis-tortion.124 6. Rules of Thumb
The relatively subtle depth cue of atmospheric perspective,
where the color of distant objects is shifted toward blue, would
conﬂict with color encoding.
6.3.6 Tilted T ext Isn’t Legibile
Another problem with the use of 3D is dramatically impaired textlegibility with most standard graphics packages that use currentdisplay technology [Grossman et al. 07]. Text fonts have beenvery carefully designed for maximum legibility when rendered onthe grid of pixels that makes up a 2D display, so that charactersas little as nine pixels high are easily readable. Although hard-ware graphics acceleration is now nearly pervasive, so that textpositioned at arbitrary orientations in 3D space can be renderedquickly , this text is usually not rendered well . As soon as a text
label is tilted in any way off of the image plane, it typically becomesblocky and jaggy. The combination of more careful rendering andvery high-resolution displays of many hundred of dots per inchmay solve this problem in the future, but legibility is a major prob-lem today.
6.3.7 Beneﬁts of 3D: Shape Perception
The great beneﬁt of using 3D comes when the viewer’s task fun-damentally requires understanding the three-dimensional geomet-ric structure of objects or scenes. In almost all of these cases,
a 3D view with interactive navigation controls to set the 3D view-point will allow users to construct a useful mental model of datasetstructure more quickly than simply using several 2D axis-alignedviews. For these tasks, all of the costs of using 3D discussed aboveare outweighed by the beneﬁt of helping the viewer build a mentalmodel of the 3D geometry.
For example, although people can be trained to comprehend
blueprints with a top view and two side views, synthesizing theinformation contained within these views to understand what acomplex object looks like from some arbitrary 3D viewpoint is a dif-ﬁcult problem that incurs signiﬁcant cognitive and memory load.The 2D blueprint views are better for the task of accurately dis-criminating the sizes of building elements, which is why they arestill heavily used in construction. However, there is considerableexperimental evidence that 3D outperforms 2D for shape under-standing tasks [St. John et al. 01].6.3. No Unjustiﬁed 3D 125
Figure 6.6. The use of 3D is well justiﬁed when the central task is shape under-
standing, as in this example of 3D streamline showing the patterns of ﬂuid ﬂow
through a volume. From [Li and Shen 07, Figure 9].
Most tasks that have inherently 3D spatial data after the ab-
straction stage fall into this category. Some classical examples are
ﬂuid ﬂow over an airplane wing, a medical imaging tomographydataset of the human body, or molecular interaction within a liv-ing cell. Figure 6.6 shows an example of streamlines in 3D ﬂuid/trianglerightsldStreamlines are discus-
sed further in Section 8.5,
and geometric navigation in
Section 11.5. ﬂow [Li and Shen 07], where geometric navigation based on 3D
rotation is a good strategy to help users understand the complexshapes quickly.
6.3.8 Justiﬁcation and Alternatives
The question of whether to use two or three channels for spatialposition has now been extensively studied. When computer-basedvis began in the late 1980s, there was a lot of enthusiasm for 3Drepresentations. As the ﬁeld matured, researchers began to bet-ter appreciate the costs of 3D approaches when used for abstractdatasets [Ware 01]. By now, the use of 3D for abstract data re-quires careful justiﬁcation. In many cases, a different choice atthe abstraction or visual encoding levels would be more appropri-ate.
Example: Cluster–Calendar Time-Series Vis
A good example is a system from van Wijk and van Selow designed to
browse time-series data [van Wijk and van Selow 99]. The dataset has two126 6. Rules of Thumb
KW
0:006:0012:0018:0024:00
hours
1 jan.5 feb.daysKW
12 mar.16 apr.21 may25 jun.30 jul.3 sep.8 oct.12 nov.17 dec.Total KW consumption ECN
0400800120016002000
(a)
(b)
Figure 6.7. 3D versus 2D. (a) A 3D representation of this time-series dataset introduces the problems of occlusion
and perspective distortion. (b) The linked 2D views of derived aggregate curves and the calendar allow direct
comparison and show more ﬁne-grained patterns. From [van Wijk and van Selow 99, Figures 1 and 4].6.3. No Unjustiﬁed 3D 127
related sets of measurements: the number of people inside and amount
of power used in an ofﬁce building, with measurements over the courseof each day for one full year. The authors compare a straightforward 3Drepresentation with a carefully designed approach using linked 2D views,which avoids the problems of occlusion and perspective distortion. Fig-ure 6.7(a) shows the straightforward 3D representation created directlyfrom the original time-series data, where each cross-section is a 2D time
series curve showing power consumption for one day, with one curve for
each day of the year along the extruded third axis. Only very large-scalepatterns such as the higher consumption during working hours and theseasonal variation between winter and summer are visible.
The ﬁnal vis designed by the authors uses multiple linked 2D views
and a different data abstraction. They created the derived data of a hier-
/trianglerightsldLinked views are dis-
cussed in Chapter 12. archical clustering of the time-series curves through an iterative process
where the most similar curves are merged together into a cluster that can
be represented by the average of the curves within it.
Figure 6.7(b) shows a single aggregate curve for each of the highest-
level groups in the clustering in the window on the right of the display.There are few enough of these aggregate curves that they can all be su-perimposed in the same 2D image without excessive visual clutter. Di-rect comparison between the curve heights at all times of the day is easybecause there is no perspective distortion or occlusion. (The cluster–
calendar vis shows the number of people in the building, rather than the
power consumption of the 3D extruded vis.)
On the left side of Figure 6.7(b) is a calendar view. Calendars are a
very traditional and successful way to show temporal patterns. The viewsare linked with shared color coding. The same large-scale patterns ofseasonal variation between summer and winter that can be seen in 3D arestill very visible, but smaller-scale patterns that are difﬁcult or impossibleto spot in the 3D view are also revealed. In this Dutch calendar, weeks are
vertical strips with the weekend at the bottom. We can identify weekends
and holidays as the nearly ﬂat teal curve where nobody is in the building,and normal weekdays as the topmost tan curve with a full house. Summerand Fridays during the winter are the brown curve with one hundred fewerpeople, and Fridays in the summer are the green curve with nearly halfof the employees gone. The blue and magenta curves show days betweenholiday times where most people also take vacation. The red curve showsthe unique Dutch holiday of Santa Claus day, where everybody gets toleave work an hour early.
While unbridled enthusiasm for 3D is no longer common, there
are indeed situations where its use is justiﬁable even for abstract
data.128 6. Rules of Thumb
Example: Layer-Oriented Time-Series Vis
Figure 6.8 shows an example that is similar on the surface to the pre-
vious one, but in this case 3D is used with care and the design is welljustiﬁed [Lopez-Hernandez et al. 10]. In this system for visualizing os-cilloscope time-series data, the user starts by viewing the data using the
traditional eye diagram where the signal is wrapped around in time and
shown as many overlapping traces. Users can spread the traces apartusing the metaphor of opening a drawer, as shown in Figure 6.8(a). Thisdrawer interface does use 3D, but with many constraints. Layers are or-thographically projected and always face the viewer. Navigation complexityis controlled by automatically zooming and framing as the user adjusts thedrawer’s orientation, as shown in Figure 6.8(b).
(a)
(b)
Figure 6.8. Careful use of 3D. (a) The user can evolve the view from the traditional
overlapping eye diagram with the metaphor of opening a drawer. (b) The interac-tion is carefully designed to avoid the difﬁculties of unconstrained 3D navigation.From [Lopez-Hernandez et al. 10, Figures 3 and 7].6.3. No Unjustiﬁed 3D 129
6.3.9 Empirical Evidence
Empirical experiments are critical in understanding user perfor-
mance, especially because of the well-documented dissociation be-
tween stated preference for 3D and actual task performance [An-dre and Wickens 95]. Experimental evidence suggests that 3D in-terfaces are better for shape understanding, whereas 2D are bestfor relative position tasks: those that require judging the precise
distances and angles between objects [St. John et al. 01]. Mosttasks involving abstract data do not beneﬁt from 3D; for exam-ple, an experiment comparing 3D cone trees to an equivalent 2Dtree browser found that the 3D interaction had a signiﬁcant timecost [Cockburn and McKenzie 00].
Designing controlled experiments that untangle the efﬁcacy of
speciﬁc interfaces that use 3D can be tricky. Sometimes the goalof the experimenter is simply to compare two alternative interfacesthat differ in many ways; in such cases it is dangerous to concludethat if an interface that happens to be 3D outperforms anotherthat happens to be 2D, it is the use of 3D that made the differ-ence. In several cases, earlier study results that were interpretedas showing beneﬁts for 3D were superseded by more careful exper-imental design that eliminated uncontrolled factors. For example,the 3D Data Mountain interface for organizing web page thumbnailimages was designed to exploit human spatial cognition and wasshown to outperform the standard 2D Favorites display in InternetExplorer [Robertson et al. 98]. However, this study left open thequestion of whether the beneﬁt was from the use of 3D or the useof the data mountain visual encoding, namely, a spatial layout al-lowing immediate access to every item in each pile of information.A later study compared two versions of Data Mountain, one with3D perspective and one in 2D, and no performance beneﬁt for 3Dwas found [Cockburn and McKenzie 01].
Another empirical study found no beneﬁts for 3D landscapes
created to reﬂect the density of a 2D point cloud, compared withsimply showing the point cloud in 2D [Tory et al. 07]. In the 3Dinformation landscape idiom, the density of the points on the plane
is computed as a derived attribute and used to construct a surfacewhose height varies according to this attribute in order to showits value in a form similar to geographic terrain.
⋆A third alterna-⋆Other names for a 3D
landscape are height ﬁeld
and terrain . tive to landscapes or points is a contour plot , where colored bands
show the outlines of speciﬁc heights. A contour plot can be used
/trianglerightsldContour plots are dis-
cussed in Section 8.4.1.alone as a 2D landscape or can be combined with 3D for a coloredlandscape. Proponents of this idiom have argued that landscapes130 6. Rules of Thumb
(a)
 (b)
 (c)
 (d)
(e)
 (f)
 (g)
Figure 6.9. Point-based displays were found to outperform information landscapes in an empirical study of visual
encodings for dimensionally reduced data. (a) Colored points. (b) Grayscale points. (c) Colored 2D landscape.
(d) Grayscale 2D landscape. (e) Colored 3D landscape. (f) Grayscale 3D landscape. (g) Height only. From [T oryet al. 07, Figure 1].
are familiar and engaging, and they have been used in several sys-
tems for displaying high-dimensional data after dimensionality re-
duction was used to reduce to two synthetic dimensions [Davidson
et al. 01, Wise et al. 95]./trianglerightsldDimensionality reduction
is discussed in Section
13.4.3.
Figure 6.9 shows the seven possibilities tested in the empirical
study comparing points to colored and uncolored landscapes. The
ﬁndings were that points were far superior to landscapes for searchand point estimation tasks and in the landscape case 2D land-scapes were superior to 3D landscapes [Tory et al. 07]. A follow-up study for a visual memory task yielded similar results [Toryet al. 09].6.4. No Unjustiﬁed 2D 131
6.4 No Unjustiﬁed 2D
Laying out data in 2D space should also be explicitly justiﬁed, com-
pared with the alternative of simply showing the data with a 1Dlist.
Lists have several strengths. First, they can show the maximal
amount of information, such as text labels, in minimal space. Incontrast, 2D layouts such as node–link representations of networkdata require considerably more space to show the same number oflabels, so they have notably lower information density.
Second, lists are excellent for lookup tasks when they are or-
dered appropriately, for example in alphabetical order when the
goal is to ﬁnd a known label. In contrast, ﬁnding a speciﬁc labelin a 2D node–link representation might require the user to huntaround the entire layout, unless a speciﬁc search capability is builtinto the vis tool.
When the task truly requires understanding the topological
structure of the network, then the beneﬁts of showing those rela-tionships explicitly outweigh the cost of the space required. How-ever, some tasks are handled well by linear lists, even if the originaldata has network structure.
6.5 Eyes Beat Memory
Using our eyes to switch between different views that are visiblesimultaneously has much lower cognitive load than consulting ourmemory to compare a current view with what was seen before.Many interaction idioms implicitly rely on the internal use of mem-ory and thus impose cognitive load on the viewer. Consider navi-gation within a single view, where the display changes to show thescene from a different viewpoint. Maintaining a sense of orienta-tion implicitly relies on using internal resources, either by keepingtrack of past navigation choices (for example, I zoomed into the
nucleus ) or by remembering past views (for example, earlier all the
stock options in the tech sector were in the top corner of the view ). In
contrast, having a small overview window with a rectangle withinit showing the position and size of the current camera viewport forthe main view is a way to show that information through an exter-nal representation easily consulted by looking at that region of thescreen, so that it can be read off by the perceptual system insteadof remembered.132 6. Rules of Thumb
6.5.1 Memory and Attention
Broadly speaking, people have two different categories of mem-
ory: long-term memory that can last a lifetime, versus short-termmemory that lasts several seconds, also known as working mem-
ory. While the capacity of long-term memory doesn’t have a strict
upper limit, human working memory is a very limited resource.When these limits are reached, people experience cognitive load
and will fail to absorb all of the information that is presented.
Human attention also has severe limits. Conscious search for
items is an operation that grows more difﬁcult with the numberof items there are to be checked. Vigilance is also a highly lim-ited resource: our ability to perform visual search tasks degradesquickly, with far worse results after several hours than in the ﬁrstfew minutes.
6.5.2 Animation versus Side-by-Side Views
Some animation-based idioms also impose signiﬁcant cognitive loadon the viewer because of implicit memory demands. Animation isan overloaded word that can mean many different things consid-ered through the lens of vis encoding and interaction. I distinguishbetween these three deﬁnitions:
•narrative storytelling, as in popular movies;
•transitions from just one state to another;
•video-style playback of a multiframe sequence: play, pause,stop, rewind, and step forward/back.
Some people have the intuition that because animation is a
powerful storytelling medium for popular movies, it should also besuitable in a vis context. However, the situation is quite different.Successful storytelling requires careful and deliberate choreogra-phy to ensure that action is only occurring in one place at a timeand the viewer’s eyes have been guided to ensure that they are
looking in the right place. In contrast, a dataset animation might
have simultaneous changes in many parts of the view.
Animation is extremely powerful when used for transitions be-
tween two dataset conﬁgurations because it helps the user main-tain context. There is considerable evidence that animated transi-tions can be more effective than jump cuts, because they help peo-ple track changes in object positions or camera viewpoints. These6.5. Eyes Beat Memory 133
transitions are most useful when only a few things change; if the
number of objects that change between frames is large, people willhave a hard time tracking everything that occurs. We are blindto changes in regions of the image that are not the focus of ourattention.
/trianglerightsldChange blindness is cov-
ered in Section 6.5.3.
Although jump cuts are hard to follow when only seen once,
giving the user control of jumping back and forth between just twoframes can be effective for detecting whether there is a localizedchange between two scenes. This blink comparator idiom was used
by the astronomer who found Pluto.
Finally, I consider animations as sequences of many frames,
where the viewer can control the playback using video-style con-trols of play, pause, stop, rewind, and sometimes single-step for-ward or backward frame by frame. I distinguish animation fromtrue interactive control, for example, navigation by ﬂying througha scene. With animation the user does not directly control whatoccurs, only the speed at which the animation is played.
The difﬁculty of multiframe animations is that making compar-
isons between frames that do not adjoin relies on internal memoryof what previous frames looked like. If changes only occur in one
place at a time, the demands on attention and internal memory aresmall. However, when many things change all over the frame andthere are many frames, we have a very difﬁcult time in trackingwhat happens. Giving people the ability to pause and replay theanimation is much better than only seeing it a single time straightthrough, but that control does not fully solve the problem.
For tasks requiring detailed comparison across many frames,
seeing all the frames at once side by side can be more effectivethan animation. The number of frames must be small enoughthat the details within each can be discerned, so this approachis typically suitable for dozens but not hundreds of frames withcurrent display resolutions. The action also should be segmentedinto meaningful chunks, rather than keyframes that are randomlychosen. Many vis idioms that use multiple views exploit this ob-servation, especially small multiples.
/trianglerightsldSmall multiples are cov-
ered in Section 12.3.2.
6.5.3 Change Blindness
The human visual system works by querying the world around ususing our eyes. Our visual system works so well that most peoplehave the intuition that we have detailed internal memory of thevisual ﬁeld that surrounds us. However, we do not. Our eyes dartaround, gathering information just in time for our need to use it, so134 6. Rules of Thumb
quickly that we do not typically notice this motion at a conscious
level.
The phenomenon of change blindness is that we fail to notice
even quite drastic changes if our attention is directed elsewhere.For example, experimenters set up a real-world interaction wheresomebody was engaged by a stranger who asked directions, onlyto be interrupted by people carrying a door who barged in betweenthem. The experimenters orchestrated a switch during this visualinterruption, replacing the questioner with another person. Re-markably, most people did not notice, even when the new ques-tioner was dressed completely differently—or was a different gen-der than the old one!
Although we are very sensitive to changes at the focus of our
attention, we are surprisingly blind to changes when our attentionis not engaged. The difﬁculty of tracking complex and widespreadchanges across multiframe animations is one of the implications ofchange blindness for vis.
6.6 Resolution over Immersion
Pixels are precious: if you are faced with a trade-off between reso-lution and immersion, resolution usually is far more important.
Immersive environments emphasize simulating realistic inter-
action and perception as closely as possible through technologysuch as stereo imagery delivered separately to each eye to en-hance depth perception, and full six-degree-of-freedom head andposition tracking so that the displays respond immediately to theuser’s physical motion of walking and moving the head around.The most common display technology is head-mounted displays,or small rooms with rear-projection displays on walls, ﬂoor, andceilings. Immersion is most useful when a sense of presence isan important aspect of the intended task. With current displayhardware, there is a trade-off between resolution , the number of
available pixels divided by the display area, and immersion , the
feeling of presence in virtual reality. The price of immersion isresolution; these displays cannot show as many pixels as state-of-the-art desktop displays of the equivalent area. The number ofpixels available on a computer display is a limited resource thatis usually the most critical constraint in vis design. Thus, it is
/trianglerightsldDisplay resolution con-
straints are discussed in
Section 1.13. extremely rare that immersion is worth the cost in resolution.
Another price of immersion is the integration of vis with the
rest of a user’s typical computer-based workﬂow. Immersive dis-6.7. Overview First, Zoom and Filter, Details on Demand 135
play environments are almost always special-purpose settings that
are a different physical location than the user’s workspace, requir-ing them to leave their usual ofﬁce and go to some other location,whether down the hall or in another building. In most cases usersstand rather than sit, so working for extended periods of time isphysically taxing compared with sitting at a desk. The most criticalproblem is that they do not have access to their standard workingenvironment of their own computer system. Without access to theusual input devices of mouse and keyboard, standard applicationssuch as web browsing, email reading, text and spreadsheet editing,and other data analysis packages are completely unusable in mostcases, and very awkward at best. In contrast, a vis system thatﬁts into a standard desktop environment allows integration withthe usual workﬂow and fast task switching between vis and otherapplications.
A compelling example of immersion is the use of virtual reality
for phobia desensitization; somebody with a fear of heights wouldneed a sense of presence in the synthetic environment in order tomake progress. However, this example is not an application of vis,since the goal is to simulate reality rather than to visually encodeinformation. The most likely case where immersion would be help-ful for vis is when the chosen abstraction includes 3D spatial data.Even in this case, the designer should consider whether a sense ofpresence is worth the penalties of lower resolution and no workﬂowintegration. It is very rare that immersion would be necessary fornonspatial, abstract data. Using 3D for visual encoding of abstractdata is the uncommon case that needs careful justiﬁcation. The
/trianglerightsldThe need for justifying 3D
for abstract data is covered
in Section 6.3. use of an immersive display in this case would require even more
careful justiﬁcation.
6.7 Overview First, Zoom and Filter, Details
on Demand
Ben Shneiderman’s inﬂuential mantra of Overview First, Zoom and
Filter, Details on Demand [Shneiderman 96] is a heavily cited de-
sign guideline that emphasizes the interplay between the need for
overview and the need to see details, and the role of data reductionin general and navigation in particular in supporting both.
A vis idiom that provides an overview is intended to give the
user a broad awareness of the entire information space. Using thelanguage of the what–why–how analysis framework, it’s an idiom136 6. Rules of Thumb
with the goal of summarize . A common goal in overview design
is to show all items in the dataset simultaneously, without any
need for navigation to pan or scroll. Overviews help the user ﬁndregions where further investigation in more detail might be produc-tive. Overviews are often shown at the beginning of the explorationprocess, to guide users in choosing where to drill down to inspectin more detail. However, overview usage is not limited to initialreconnaissance; it’s very common for users to interleave the useof overviews and detail views by switching back and forth betweenthem many times.
When the dataset is sufﬁciently large, some form of reduce ac-
tion must be used in order to show everything at once. Overviewcreation can be understood in terms of both ﬁltering and aggre-gation. A simple way to create overviews is by zooming out ge-ometrically, so that the entire dataset is visible within the frame.Each object is drawn smaller, with less room to show detail. In thissense, overviews are created by removing all ﬁltering: an overviewis created by changing from a zoomed-in view where some itemsare ﬁltered out, to a zoomed-out view where all items are shown.When the number of items in a dataset is large enough, showingan overview of the entire dataset in a single screen using one markper item is impossible, even if the mark size is decreased to a sin-gle pixel. When the number of items to draw outstrips the numberof available pixels, the number of marks to show must be reducedwith aggregation. Moreover, even for datasets of medium size, ex-
/trianglerightsldAggregation is discussed
in Section 13.4. plicitly designing an overview display using a more sophisticatedapproach than simple geometric zooming can be fruitful. These
custom overviews are similar in spirit to semantic zooming, in thatthe representation of the items is qualitatively different rather thansimply being drawn smaller than the full-detail versions. These
/trianglerightsldGeometric and semantic
zooming are discussed in
Section 11.5. kinds of overviews often use dynamic aggregation that is implicitly
driven by navigation, rather than being explicitly chosen by theuser.
There is no crisp line dividing an “overview” from an “ordinary”
vis idiom, because many idioms provide some form of overview orsummary. However, it’s often useful to make a relative distinctionbetween a less detailed view that summarizes a lot of data and amore detailed view that shows a smaller number of data items with
more information about each one. The former one is clearly theoverview , the latter one is the detail view . It’s particularly obvious
how to distinguish between these when the idiom design choice ofmultiple views is being used; the mantra is particularly applicablewhen the detail view pops up in response to a select action by the6.8. Responsiveness Is Required 137
user, but it’s also common for the detail view to be permanently
visible side by side with the overview. There two other major fam-/trianglerightsldChapter 12 covers multi-
ple views.ilies of idioms that support overviewing. One is to use a single
view that dynamically changes over time by providing support for
reduce actions such as zooming and ﬁltering; then that single view
sometimes acts as an overview and sometimes as a detail view. The/trianglerightsldChapter 13 covers ap-
proaches to data reduction.
third choice is to embed both detailed focus and overview contextinformation together within a single view.
/trianglerightsldChapter 14 covers fo-
cus+context idioms.This mantra is most helpful when dealing with datasets of mod-
erate size. When dealing with enormous datasets, creating a useful
overview for top-down exploration may not be feasible. In sloganform, an alternative approach is Search, Show Context, Expand on
Demand [van Ham and Perer 09], where search results provide the
starting point for browsing of local neighborhoods.
6.8 Responsiveness Is Required
The latency of interaction, namely, how much time it takes for the
system to respond to the user action, matters immensely for inter-action design. Our reaction to latency does not simply occur on acontinuum, where our irritation level gradually rises as things takelonger and longer. Human reaction to phenomena is best modeledin terms of a series of discrete categories, with a different timeconstant associated with each one. A system will feel responsive ifthese latency classes are taken into account by providing feedbackto the user within the relevant time scale. The three categoriesmost relevant for vis designers are shown in Table 6.1.
The perceptual processing time constant of one-tenth of a sec-
ond is relevant for operations such as screen updates. The immedi-ate response time constant of one second is relevant for operationssuch as visual feedback showing what item that user has selectedwith a mouse click, or the length of time for an animated transi-tion from one layout to another. The brief task time constant of ten
Time Constant
Value (in seconds)
perceptual processing 0.1
immediate response 1
brief tasks 10
Table 6.1. Human response to interaction latency changes dramatically at these
time thresholds. After [Card et al. 91, T able 3].138 6. Rules of Thumb
seconds is relevant for breaking down complex tasks into simpler
pieces; a good granularity for the smallest pieces is this brief tasktime.
6.8.1 Visual Feedback
From the user’s point of view, the latency of an interaction isthe time between their action and some feedback from the sys-tem indicating that the operation has completed. In a vis system,that feedback would most naturally be some visual indication ofstate change within the system itself, rather than cumbersome ap-proaches such as printing out status indications at the console ora popup dialog box conﬁrmation that would interfere with the ﬂowof exploration.
The most obvious principle is that the user should indeed have
some sort of conﬁrmation that the action has completed, ratherthan being left dangling wondering whether the action is still inprogress, or whether the action never started in the ﬁrst place (forexample, because they missed the target and clicked on the back-ground rather than the intended object). Thus, feedback such ashighlighting a selected item is a good way to conﬁrm that the de-sired operation has completed successfully. In navigation, feed-back would naturally come when the user sees the new frameis drawn from the changed viewpoint. Visual feedback shouldtypically take place within the immediate response latency class:around one second.
Another principle is that if an action could take signiﬁcantly
longer than a user would naturally expect, some kind of progressindicator should be shown to the user. A good rule of thumb forsigniﬁcantly longer is crossing from one latency class into another,as shown in Table 6.1.
6.8.2 Latency and Interaction Design
Successful interaction design for a vis system depends on hav-ing a good match between the latencies of the low-level interaction
mechanism, the visual feedback mechanism, the system update
time, and the cognitive load of operation itself.
For example, consider the operation of seeing more details for
an item and the latency difference between three different low-levelinteraction mechanisms for doing so. Clicking on the item is slow-est, because the user must move the mouse toward the target lo-cation, stop the motion in the right place, and press down on the6.8. Responsiveness Is Required 139
mouse. Mouseover hover, where the cursor is placed over the ob-
ject for some short period of dwell time but no click is required,may or may not be faster depending on the dwell time. Mouseoveractions with no dwell time requirement, where the action is trig-gered by the cursor simply crossing the object, are of course thefastest because the second step is also eliminated and only the ﬁrststep needs to take place.
For visual feedback, consider three different mechanisms for
showing the information. One is showing the information on aﬁxed detail pane at the side of the screen. In order to see the in-formation, the user’s eyes need to move from the current cursorlocation to the side of the screen, so this operation has relativelyhigh latency for making use of the visual feedback. On the otherhand, from a visual encoding point of view, an advantage is thata lot of detail information can be shown without occluding any-thing else in the main display. A second feedback mechanism isa popup window at the current cursor location, which is faster touse since there is no need to move the eyes away from trackingthe cursor. Since placing information directly in the view might oc-clude other objects, there is a visual encoding cost to this choice. Athird mechanism is a visual highlight change directly in the view,for instance by highlighting all neighbors within the graph that areone hop from the graph node under the cursor through a colorchange.
System update time is another latency to consider. With tiny
datasets stored completely locally, update time will be negligible
for any of these options. With larger datasets, the time to redrawthe entire view could be considerable unless the rendering
⋆frame- ⋆The term rendering is
used in computer graphics
for drawing an image.work has been designed to deliver frames at a guaranteed rate.
Similarly, scalable rendering frameworks can support fast updatefor changing a few items or a small part of the display without re-drawing the entire screen, but most graphics systems do not offerthis functionality by default. Thus, designing systems to guar-antee immediate response to user actions can require signiﬁcantalgorithmic attention. With distributed datasets, obtaining detailsmay require a round trip from the client to the server, possiblytaking several seconds on a congested network.
When systems are designed so that all of these latencies are
well matched, the user interacts ﬂuidly and can stay focused onhigh-level goals such as building an internal mental model of thedataset. When there is a mismatch, the user is jarred out of astate of ﬂow [Csikszentmihalyi 91] by being forced to wait for thesystem.140 6. Rules of Thumb
6.8.3 Interactivity Costs
Interactivity has both power and cost. The beneﬁt of interaction
is that people can explore a larger information space than can beunderstood in a single static image. However, a cost to interaction
is that it requires human time and attention. If the user mustexhaustively check every possibility, use of the vis system maydegenerate into human-powered search. Automatically detectingfeatures of interest to explicitly bring to the user’s attention via thevisual encoding is a useful goal for the vis designer. However, if thetask at hand could be completely solved by automatic means, therewould be no need for a vis in the ﬁrst place. Thus, there is alwaysa trade-off between ﬁnding automatable aspects and relying on thehuman in the loop to detect patterns.
6.9 Get It Right in Black and White
Maureen Stone has advocated the slogan Get It Right in Black and
White as a design guideline for effective use of color [Stone 10].
That is, ensure that the most crucial aspects of visual represen-tation are legible even if the image is transformed from full colorto black and white. Do so by literally checking your work in blackand white, either with image processing or by simply printing out ascreenshot on a black and white printer. This slogan suggests en-coding the most important attribute with the luminance channel toensure adequate luminance contrast and considering the hue andsaturation channels as secondary sources of information./trianglerightsldThe principles of us-
ing color to visually encode
data are discussed in Sec-tion 10.2. Figure 12.13shows an example of ex-plicitly checking luminancecontrast between elements
on different layers.
6.10 Function First, Form Next
The best vis designs should shine in terms of both form and func-
tion; that is, they should be both beautiful and effective. Neverthe-less, in this book, I focus on function.
My rationale is that given an effective but ugly design, it’s possi-
ble to reﬁne the form to make it more beautiful while maintainingthe base of effectiveness. Even if the original designer of the vis hasno training in graphic design, collaboration is possible with peoplewho do have that background.
In contrast, given a beautiful and ineffective design, you will
probably need to toss it out and start from scratch. Thus, I don’tadvocate a “form ﬁrst” approach, because progressive reﬁnement6.11. Further Reading 141
is usually not possible. My argument mirrors the claims I made in
the ﬁrst chapter about the size of the vis design space and the factthat most designs are ineffective.
Equally important is the point that I don’t advocate “form never”:
visual beauty does indeed matter, given that vis makes use of hu-man visual perception. Given the choice of two equally effectivesystems, where one is beautiful and one is ugly, people will preferthe better form. Moreover, good visual form enhances the effective-ness of visual representations.
I don’t focus on teaching the principles and practice of graphic
design in this book because they are covered well by many othersources. I focus on the principles of vis effectiveness because ofthe lack of other resources.
6.11 Further Reading
No Unjustiﬁed 3D The differences between planar and depth spatial
perception and the characteristics of 3D depth cues are dis-cussed at length in both of Ware’s books [Ware 08, Ware 13].An in-depth discussion of the issues of 2D versus 3D [St. Johnet al. 01] includes references to many previous studies inthe human factors and air trafﬁc control literature includingthe extensive work of Wickens. Several careful experimentsoverturned previous claims of 3D beneﬁts over 2D [Cockburnand McKenzie 00, Cockburn and McKenzie 01, Cockburn andMcKenzie 04].
Memory Ware’s textbook is an excellent resource for memory and at-
tention as they relate to vis [Ware 13], with much more detail
than I provide here. A recent monograph contains an inter-esting and thorough discussion of supporting and exploitingspatial memory in user interfaces [Scarr et al. 13].
Animation An inﬂuential paper on incorporating the principles of
hand-drawn animation into computer graphics discusses theimportance of choreography to guide the viewer’s eyes duringnarrative storytelling [Lasseter 87]. A meta-review of anima-tion argues that many seemingly promising study results areconfounded by attempts to compare incommensurate situa-tions; the authors ﬁnd that small multiples are better thananimation if equivalent information is shown [Tversky et al. 02]and the segmentation is carefully chosen [Zacks and Tver-sky 03]. An empirical study found that while trend anima-142 6. Rules of Thumb
tion was fast and enjoyable when used for presentation it did
lead to errors, and it was signiﬁcantly slower than both smallmultiples and trace lines for exploratory analysis [Robertsonet al. 08].
Change Blindness A survey paper is a good starting point for the
change blindness literature [Simons 00].
Overview, Zoom and Filter, Details on Demand This early and inﬂuen-
tial mantra about overviews is presented in a very readablepaper [Shneiderman 96]. More recently, a synthesis reviewanalyzes the many ways that overviews are used in infovis[Hornbæk and Hertzum 11].
Responsiveness Is Required Card pioneered the discussion of latency
classes for vis and human–computer interaction [Card et al. 91];
an excellent book chapter covering these ideas appears in avery accessible book on interface design [Johnson 10, Chap-ter 12]. The costs of interaction are discussed in a synthesisreview [Lam 08] and a proposed framework for interaction [Yiet al. 07].
Get It Right in Black and White A blog post on Get It Right in Black
and White is a clear and concise starting point for the topic[Stone 10].
Function First, Form Next A very accessible place to start for basic
graphic design guidelines is The Non-Designer’s Design Book
[Williams 08].This page intentionally left blankThis page intentionally left blankArrange Tables
Express Values
Separate, Order, Align Regions
Axis Orientation
Layout Density
Dense Space-FillingSeparate Order Align
1 Key 2  Keys 3 Keys Many Keys
List Recursive Subdivision Volume Matrix
Rectilinear Parallel Radial
Figure 7.1. Design choices for arranging tables.Arrange T ablesChapter 7
7.1 The Big Picture
Figure 7.1 shows the four visual encoding design choices for how
to arrange tabular data spatially. One is to express values. Theother three are to separate, order, and align regions. The spatialorientation of axes can be rectilinear, parallel, or radial. Spatiallayouts may be dense, and they may be space-ﬁlling./trianglerightsld A ﬁfth arrangement
choice, to use a given spa-
tial layout, is not an option
for nonspatial information; it
is covered in Chapter 8.
7.2 Why Arrange?
The arrange design choice covers all aspects of the use of spatial
channels for visual encoding. It is the most crucial visual encod-
ing choice because the use of space dominates the user’s mentalmodel of the dataset. The three highest ranked effectiveness chan-nels for quantitative and ordered attributes are all related to spatialposition: planar position against a common scale, planar positionalong an unaligned scale, and length. The highest ranked effectiv-ness channel for categorical attributes, grouping items within thesame region, is also about the use of space. Moreover, there areno nonspatial channels that are highly effective for all attributetypes: the others are split into being suitable for either orderedor categorical attributes, but not both, because of the principle ofexpressiveness.
/trianglerightsldThe primacy of the spa-
tial position channels is dis-
cussed at length in Chap-ter 5, as are the principles
of effectiveness and expres-
siveness.
7.3 Arrange by Keys and Values
The distinction between key and value attributes is very relevant to
visually encoding table data. A key is an independent attribute that
can be used as a unique index to look up items in a table, while avalue is a dependent attribute: the value of a cell in a table. Key/trianglerightsldSee Section 2.6.1 for
more on keys and values.
attributes can be categorical or ordinal, whereas values can be all
145146 7. Arrange T ables
three of the types: categorical, ordinal, or quantitative. The unique
values for a categorical or ordered attribute are called levels ,t o
avoid the confusion of overloading the term value .
The core design choices for visually encoding tables directly re-
late to the semantics of the table’s attributes: how many keys andhow many values does it have? An idiom could only show val-ues, with no keys; scatterplots are the canonical example of show-ing two value attributes. An idiom could show one key and one
value attribute; bar charts are the best-known example. An idiomcould show two keys and one value; for example, heatmaps. Idiomsthat show many keys and many values often recursively subdividespace into many regions, as with scatterplot matrices.
While datasets do only have attributes with value semantics,
it would be rare to visually encode a dataset that has only keyattributes. Keys are typically used to deﬁne a region of space foreach item in which one or more value attributes are shown.
7.4 Express: Quantitative Values
Using space to express quantitative attributes is a straightforwarduse of the spatial position channel to visually encode data. Theattribute is mapped to spatial position along an axis.
In the simple case of encoding a single value attribute, each item
is encoded with a mark at some position along the axis. Additionalattributes might also be encoded on the same mark with othernonspatial channels such as color and size. In the more complexcase, a composite glyph object is drawn, with internal structure
that arises from multiple marks. Each mark lies within a subregionin the glyph that is visually encoded differently, so the glyph canshow multiple attributes at once.
/trianglerightsldGlyphs and views are
discussed further in Sec-
tion 12.4.
Example: Scatterplots
The idiom of scatterplots encodes two quantitative value variables using
both the vertical and horizontal spatial position channels, and the mark
type is necessarily a point.
Scatterplots are effective for the abstract tasks of providing overviews
and characterizing distributions, and speciﬁcally for ﬁnding outliers andextreme values. Scatterplots are also highly effective for the abstract taskof judging the correlation between two attributes. With this visual en-coding, that task corresponds the easy perceptual judgement of noticing7.4. Express: Quantitative Values 147
Figure 7.2. Scatterplot. Each point mark represents a country, with horizontal
and vertical spatial position encoding the primary quantitative attributes of life ex-
pectancy and infant mortality. The color channel is used for the categorical countryattribute and the size channel for quantitative population attribute. From [Robert-son et al. 08, Figure 1c].
whether the points form a line along the diagonal. The stronger the cor-
relation, the closer the points fall along a perfect diagonal line; positivecorrelation is an upward slope, and negative is downward. Figure 7.2shows a highly negatively correlated dataset.
Additional transformations can also be used to shed more light on the
data. Figure 7.3(a) shows the relationship between diamond price andweight. Figure 7.3(b) shows a scatterplot of derived attributes createdby logarithmically scaling the originals; the transformed attributes arestrongly positively correlated.148 7. Arrange T ables
(a)
 (b)
Figure 7.3. Scatterplots. (a) Original diamond price/carat data. (b) Derived log-scale attributes are highly positively
correlated. From [Wickham 10, Figure 10].
When judging correlation is the primary intended task, the derived
data of a calculated regression line is often superimposed on the raw scat-
terplot of points, as in Figures 7.3(b) and 1.3.
Scatterplots are often augmented with color coding to show an addi-
tional attribute. Size coding can also portray yet another attribute; size-coded scatterplots are sometimes called bubble plots . Figure 7.2 shows an
example of demographic data, plotting infant mortality on the vertical axisagainst life expectancy on the horizontal axis.
The scalability of a scatterplot is limited by the need to distinguish
points from each other, so it is well suited for dozens or hundreds of items.
The table below summarizes this discussion in terms of a what–why–
how analysis instance. All of the subsequent examples will end with asimilar summary table.
Idiom
Scatterplots
What: Data T able: two quantitative value attributes.
How: Encode Express values with horizontal and vertical spatial
position and point marks.
Why: T ask Find trends, outliers, distribution, correlation; locateclusters.
Scale Items: hundreds.7.5. Separate, Order, and Align: Categorical Regions 149
7.5 Separate, Order, and Align:
Categorical Regions
The use of space to encode categorical attributes is more complex
than the simple case of quantitative attributes where the valuecan be expressed with spatial position. Spatial position is an or-dered magnitude visual channel, but categorical attributes haveunordered identity semantics. The principle of expressivenesswould be violated if they are encoded with spatial position.
The semantics of categorical attributes does match up well with
the idea of a spatial region : regions are contiguous bounded areas
that are distinct from each other. Drawing all of the items with thesame values for a categorical attribute within the same region usesspatial proximity to encode the information about their similarity,in a way that adheres nicely to the expressiveness principle. Thechoice to separate into regions still leaves enormous ﬂexibility inhow to encode the data within each region: that’s a different designchoice. However, these regions themselves must be given spatialpositions on the plane in order to draw any speciﬁc picture.
The problem becomes easier to understand by breaking down
the distribution of regions into three operations: separating intoregions, aligning the regions, and ordering the regions. The sepa-ration and the ordering always need to happen, but the alignmentis optional. The separation should be done according to an at-tribute that is categorical, whereas alignment and ordering shouldbe done by some other attribute that is ordered. The attributeused to order the regions must have ordered semantics, and thusit cannot be the categorical one that was used to do the separa-tion. If alignment is done, the ordered attribute used to control thealignment between regions is sometimes the same one that is used
to encode the spatial position of items within the region. It’s also
possible to use a different one.
7.5.1 List Alignment: One Key
With a single key, separating into regions using that key yieldsone region per item. The regions are frequently arranged in aone-dimensional list alignment , either horizontal or vertical. The
view itself covers a two-dimensional area: the aligned list of itemsstretches across one of the spatial dimensions, and the region inwhich the values are shown stretches across the other.150 7. Arrange T ables
Example: Bar Charts
The well-known bar chart idiom is a simple initial example. Figure 7.4
shows a bar chart of approximate weights on the vertical axis for eachof three animal species on the horizontal axis. Analyzing the visual en-coding, bar charts use a line mark and encode a quantitative value at-
tribute with one spatial position channel. The other attribute shown inthe chart, animal species, is a categorical key attribute. Each line markis indeed in a separate region of space, and there is one for each level ofthe categorical attribute. These line marks are all aligned within a com-mon frame, so that the highest-accuracy aligned position channel is usedrather than the lower-accuracy unaligned channel. In Figure 7.4(a) theregions are ordered alphabetically by species name. Formally, the alpha-betical ordering of the names should be considered a derived attribute.This frequent default choice does have the beneﬁt of making lookup byname easy, but it often hides what could be meaningful patterns in thedataset. Figure 7.4(b) shows this dataset with the regions ordered by thevalues of the same value attribute that is encoded by the bar heights,animal weight. This kind of data-driven ordering makes it easier to seedataset trends. Bar charts are also well suited for the abstract task oflooking up individual values.
The scalability issues with bar charts are that there must be enough
room on the screen to have white space interleaved between the bar linemarks so that they are distinguishable. A bar corresponds to a level of thecategorical key attribute, and it’s common to show between several anddozens of bars. In the limit, a full-screen chart with 1000 pixels couldhandle up to hundreds of bars, but not thousands.
100
75
50
25
0     
Animal Type
(a)100
7550
25
0     
Animal Type
(b)
Figure 7.4. Bar chart. The key attribute, species , separates the marks along
the horizontal spatial axis. The value attribute, weight , expresses the value with
aligned vertical spatial position and line marks. (a) Marks ordered alphabetically
according to species name. (b) Marks ordered by the weight attribute used for barheights.7.5. Separate, Order, and Align: Categorical Regions 151
Idiom Bar Charts
What: Data T able: one quantitative value attribute, one categori-
cal key attribute.
How: Encode Line marks, express value attribute with aligned ver-tical position, separate key attribute with horizontalposition.
Why: T ask Lookup and compare values.
Scale Key attribute: dozens to hundreds of levels.
Example: Stacked Bar Charts
Astacked bar chart uses a more complex glyph for each bar, where multiple
sub-bars are stacked vertically. The length of the composite glyph stillencodes a value, as in a standard bar chart, but each subcomponent also
encodes a length-encoded value. Stacked bar charts show information
about multidimensional tables, speciﬁcally a two-dimensional table withtwo keys. The composite glyphs are arranged as a list according to aprimary key. The other secondary key is used in constructing the verticalstructure of the glyph itself. Stacked bar charts are an example of a listalignment used with more than one key attribute. They support the taskof lookup according to either of the two keys.
Stacked bar charts typically use color as well as length coding. Each
subcomponent is colored according to the same key that is used to deter-mine the vertical ordering; since the subcomponents are all abutted endto end without a break and are the same width, they would not be dis-tiguishable without different coloring. While it would be possible to useonly black outlines with white ﬁll as the rectangles within a bar, com-paring subcomponents across different bars would be considerably moredifﬁcult.
Figure 7.5 shows an example of a stacked bar chart used to inspect
information from a computer memory proﬁler. The key used to distributecomposite bars along the axis is the combination of a processor and aprocedure. The key used to stack and color the glyph subcomponents isthe type of cache miss; the height of each full bar encodes all cache missesfor each processor–procedure combination.
Each component of the bar is separately stacked, so that the full bar
height shows the value for the combination of all items in the stack. Theheights of the lowest bar component and the full combined bar are botheasy to compare against other bars because they can be read off againstthe ﬂat baseline; that is, the judgement is position against a commonscale. The other components in the stack are more difﬁcult to compare152 7. Arrange T ables
Figure 7.5. Stacked bar chart. The Thor memory proﬁler shows cache misses
stacked and colored by miss type. From [Bosch 01, Figure 4.1].
across bars because their starting points are not aligned to a common
scale. Thus, the order of stacking is signiﬁcant for the kinds of patternsthat are most easily visible, in addition to the ordering of bars across themain axis, as with standard bar charts./trianglerightsldStacked bars are typi-
cally used for absolute data;
relative proportions of partsto a whole can be shown
with a normalized stacked
bar chart, where each barshows the same informationas in an entire pie chart, asdiscussed in Section 7.6.3.The scalability of stacked bar charts is similar to standard bar charts
in terms of the number of categories in the key attribute distributed across
the main axis, but it is more limited for the key used to stack the subcom-ponents within the glyph. This idiom works well with several categories,with an upper limit of around one dozen.7.5. Separate, Order, and Align: Categorical Regions 153
Idiom Stacked Bar Charts
What: Data Multidimensional table: one quantitative value at-
tribute, two categorical key attributes.
How: Encode Bar glyph with length-coded subcomponents ofvalue attribute for each category of secondary keyattribute. Separate bars by category of primary keyattribute.
Why: T ask Part-to-whole relationship, lookup values, ﬁndtrends.
Scale Key attribute (main axis): dozens to hundreds of lev-els. Key attribute (stacked glyph axis): several to onedozen
Example: Streamgraphs
Figure 7.6 shows a more complex generalized stacked graph display idiom
with a dataset of music listening history, with one time series per artist
counting the number of times their music was listened to each week [By-ron and Wattenberg 08]. The streamgraph idiom shows derived geometry
that emphasizes the continuity of the horizontal layers that represent theartists, rather than showing individual vertical glyphs that would empha-size listening behavior at a speciﬁc point in time.
1The derived geome-
try is the result of a global computation, whereas individual glyphs canbe constructed using only calculations about their own local region. Thestreamgraph idiom emphasizes the legibility of the individual streams witha deliberately organic silhouette, rather than using the horizontal axis as
Figure 7.6. Streamgraph of music listening history. From [Byron and Wattenberg 08, Figure 0].
1In this case, the main axis showing the quantitative time attribute is horizon-
tal; both streamgraphs and stacked bar charts can be oriented either vertically or
horizontally.154 7. Arrange T ables
(a)
(b)
Figure 7.7. Streamgraphs with layers ordered by different derived attributes. (a)
Volatility of artist’s popularity. (b) Onset time when artist’s music of ﬁrst gained
attention. From [Byron and Wattenberg 08, Figure 15].
the baseline. The shape of the layout is optimized as a trade-off between
multiple factors, including the external silhouette of the entire shape, thedeviation of each layer from the baseline, and the amount of wiggle inthe baseline. The order of the layers is computed with an algorithm that
emphasizes a derived value; Figure 7.7 shows the difference between sort-
ing by the volatility of the artist’s popularity, as shown in Figure 7.7(a),and the onset time when they begin to gain attention, as shown in Fig-ure 7.7(b).
Streamgraphs scale to a larger number of categories than stacked bar
charts, because most layers do not extend across the entire length of thetimeline.
Idiom
Streamgraphs
What: Data Multidimensional table:
one quantitative value attribute (counts), one or-dered key attribute (time), one categorical key at-tribute (artist).
What: Derived One quantitative attribute (for layer ordering).
How: Encode Use derived geometry showing artist layers acrosstime, layer height encodes counts.
Scale Key attributes (time, main axis): hundreds of timepoints. Key attributes (artists, short axis): dozens tohundreds7.5. Separate, Order, and Align: Categorical Regions 155
Example: Dot and Line Charts
The dot chart idiom is a visual encoding of one quantitative attribute using
spatial position against one categorical attribute using point marks, rather
than the line marks of a bar chart.⋆Figure 7.8(a) shows a dot chart of cat ⋆ The terms dot chart
and dot plot are some-
times used as synonyms
and have been overloaded.I use dot chart here for
the idiom popularized byCleveland [Becker et al. 96,
Cleveland and McGill 84a],
whereas Wilkinson [Wilkin-son 99] uses dot plot for
an idiom that shows distri-butions in a way similar to
the histograms discussed in
Section 13.4.1.weight over time with the ordered variable of year on the horizontal axis
and the quantitative weight of a speciﬁc cat on the vertical axis.
One way to think about a dot chart is like a scatterplot where one
of the axes shows a categorical attribute, rather than both axes showingquantitative attributes. Another way to think about a dot chart is like abar chart where the quantitative attribute is encoded with point marksrather than line marks; this way matches more closely with its standarduse.
The idiom of line charts augments dot charts with line connection
marks running between the points. Figure 7.8(b) shows a line chart forthe same dataset side by side with the dot chart, plotting the weight of acat over several years. The trend of constantly increasing weight, followedby loss after a veterinarian-imposed diet regime in 2010, is emphasized bythe connecting lines.
Idiom
Dot Charts
What: Data T able: one quantitative value attribute, one ordered
key attribute.
How: Encode Express value attribute with aligned vertical positionand point marks. Separate/order into horizontal re-gions by key attribute.
20
1510
50     
Year
(a)201510
50     
Year
(b)
Figure 7.8. Line charts versus dot charts. (a) Dot charts use a point mark to
show the value for each item. (b) Line charts use point marks connected by lines
between them.156 7. Arrange T ables
Idiom Line Charts
What: Data T able: one quantitative value attribute, one ordered
key attribute.
How: Encode Dot chart with connection marks between dots.
Why Show trend.
Scale Key attribute: hundreds of levels.
Line charts, dot charts, and bar charts all show one value at-
tribute and one key attribute with a rectilinear spatial layout. All of
these chart types are often augmented to show a second categori-cal attribute using color or shape channels. They use one spatialposition channel to express a quantitative attribute, and use theother direction for a second key attribute. The difference is thatline charts also use connection marks to emphasize the orderingof the items along the key axis by explicitly showing the relation-ship between one item and the next. Thus, they have a strongerimplication of trend relationships, making them more suitable forthe abstract task of spotting trends.
Line charts should be used for ordered keys but not categor-
ical keys. A line chart used for categorical data violates the ex-pressiveness principle, since it visually implies a trend where onecannot exist. This implication is so strong that it can overridecommon knowledge. Zacks and Tversky studied how people an-swered questions about the categorical data type of gender versusthe quantitative data type of age, as shown in Figure 7.9 [Zacks andTversky 99]. Line charts for quantitative data elicited appropriatetrend-related answers, such as “Height increases with age”. Barcharts for quantitative data elicited equally appropriate discrete-comparison answers such as “Twelve year olds are taller than tenyear olds”. However, line charts for categorical data elicited inap-propriate trend answers such as “The more male a person is, thetaller he/she is”.
When designing a line chart, an important question to consider
is its aspect ratio : the ratio of width to height of the entire plot.
While many standard charting packages simply use a square orsome other ﬁxed size, in many cases this default choice hides data-set structure. The relevant perceptual principle is that our abilityto judge angles is more accurate at exact diagonals than at arbi-trary directions. We can easily tell that an angle like 43
◦is off from
the exact 45◦diagonal, whereas we cannot tell 20◦from 22◦. The7.5. Separate, Order, and Align: Categorical Regions 157
Female                  Male60
50 403020
10
0     
Female                  Male6050 403020
10
0     
10-year-olds      12-year-olds6050 40302010
0     6050 40302010
0     
10-year-olds      12-year-olds
Figure 7.9. Bar charts and line charts both encode a single attribute. Bar charts
encourage discrete comparisons, while line graphs encourage trend assessments.
Line charts should not be used for categorical data, as in the upper right, becausetheir implications are misleading. After [Zacks and Tversky 99, Figure 2].
idiom of banking to 45◦computes the best aspect ratio for a chart
in order to maximize the number of line segments that fall close
to the diagonal. Multiscale banking to 45◦automatically ﬁnds a
set of informative aspect ratios using techniques from signal pro-cessing to analyze the line graph in the frequency domain, with
the derived variable of the power spectrum. Figure 7.10 shows the
classic sunspot example dataset. The aspect ratio close to 4 inFigure 7.10(a) shows the classic low-frequency oscillations in themaximum values of each sunspot cycle. The aspect ratio close to22 in Figure 7.10(b) shows that many cycles have a steep onsetfollowed by a more gradual decay. The blue line graphs the data
itself, while the red line is the derived locally weighted regression
line showing the trend.
7.5.2 Matrix Alignment: T wo Keys
Datasets with two keys are often arranged in a two-dimensionalmatrix alignment where one key is distributed along the rows and158 7. Arrange T ables
(a)
(b)
Figure 7.10. Sunspot cycles. The multiscale banking to 45◦idiom exploits our
orientation resolution accuracy at the diagonal. (a) An aspect ratio close to 4
emphasizes low-frequency structure. (b) An aspect ratio close to 22 shows higher-frequency structure: cycle onset is mostly steeper than the decay. From [Heer andAgrawala 06, Figure 5].
the other along the columns, so a rectangular cell in the matrix is
the region for showing the item values.
Example: Cluster Heatmaps
The idiom of heatmaps is one of the simplest uses of the matrix alignment:
each cell is fully occupied by an area mark encoding a single quantitative
value attribute with color. Heatmaps are often used with bioinformat-
ics datasets. Figure 7.11 shows an example where the keys are genesand experimental conditions, and the quantitative value attribute is theactivity level of a particular gene in a particular experimental conditionas measured by a microarray. This heatmap uses a diverging red–greencolormap, as is common in the genomics domain. (In this domain thereis a strong convention for the meaning of red and green that arose fromraw images created by the optical microarray sensors that record ﬂuores-cence at speciﬁc wavelengths. Unfortunately, this choice causes problemsfor colorblind users.) The genes are a categorical attribute; experimental
/trianglerightsldSee Section 10.3 for
more on colormap design
and Section 10.3.4 forthe particular problem ofcolorblind-safe design.conditions might be categorical or might be ordered, for example if the
experiments were done at successive times.
The beneﬁt of heatmaps is that visually encoding quantitative data
with color using small area marks is very compact, so they are good for7.5. Separate, Order, and Align: Categorical Regions 159
E217S299R783
E217S299R784
E217S300R787
E217S300R786
E217S300R785
E217S299R782
E111S150R567
E199S255R449
E199S255R448
E199S255R450E202S185R546E202S196R564
E202S192R557E202S188R552
E202S185R545E111S150R568
E202S190R553
E111S150R566
E144S184R737
E202S186R548
E202S186R549E202S186R547
E202S192R556
E144S184R738
E202S196R562
E202S194R560E202S188R550E202S192R558
E202S190R554E202S185R544
E202S196R563E202S188R551
E202S194R559
E189S232R190
E189S232R3861452475_at1424605_at1421396_at1459124_at1426981_at1448312_at1437339_s_at1438248_at1444147_at1437453_s_at1416965_at1447991_at1448240_at1418518_at1447992_s_at1428305_at1431386_s_at1431385_a_at1425824_a_atE202S194R561E202S190R555
Figure 7.11. Cluster heatmap. A heatmap provides a compact summary of a
quantitative value attribute with 2D matrix alignment by two key attributes and small
area marks colored with a diverging colormap. The cluster heatmap includes treesdrawn on the periphery showing how the matrix is ordered according to the deriveddata of hierarchical clusterings on its rows and columns.
providing overviews with high information density. The area marks in a
heatmap are often several pixels on a side for easy distinguishability, soa matrix of 200 ×200 with 40,000 items is easily handled. The limit
is area marks of a single pixel, for a dense heatmap showing one million
items. Thus, the scalability limits are hundreds of levels for each of the two
categorical key attributes. In contrast, only a small number of differentlevels of the quantitative attribute can be distinguishable, because of thelimits on color perception in small noncontiguous regions: between 3 and11 bins.
2
2Again, all of the scalability analyses in this book related to screen-space limits
assume a standard display size of 1000 ×1000, for a total of one million available
pixels.160 7. Arrange T ables
The cluster heatmap idiom combines the basic heatmap with matrix
reordering , where two attributes are reordered in combination.⋆The goal⋆There are many syn-
onyms for matrix reorder-
ing, including matrix per-
mutation ,seriation ,ordi-
nation ,biclustering ,co-
clustering , and two-mode
clustering . Matrix re-
ordering has been studied
in many different literaturesbeyond vis including car-tography, statistics, opera-tions research, data min-
ing, bioinformatics, ecology,
psychology, sociology, andmanufacturing.of matrix reordering is to group similar cells in order to check for large-
scale patterns between both attributes, just as the goal of reordering asingle attribute is to see trends across a single one.
Acluster heatmap is the juxtaposed combination of a heatmap and two
dendrograms showing the derived data of the cluster hierarchies used in
the reodering. A cluster hierarchy encapsulates the complete history of
how a clustering algorithm operates iteratively. Each leaf represents a
cluster of a single item; the interior nodes record the order in which clus-ters are merged together based on similarity, with the root representingthe single cluster of all items. A dendrogram is a visual encoding of tree
data with the leaves aligned so that the interior branch heights are easy tocompare. The ﬁnal order used for the rows and the columns of the matrixview is determined by traversing the leaves in the trees.
/trianglerightsldHierarchical clustering is
further discussed in Sec-
tion 13.4.1.Idiom Heatmaps
What: Data T able: two categorical key attributes (genes, condi-
tions), one quantitative value attribute (activity levelfor gene in condition).
How: Encode 2D matrix alignment of area marks, diverging color-map.
Why: T ask Find clusters, outliers; summarize.
Scale Items: one million. Categorical attribute levels: hun-dreds. Quantitative attribute levels: 3–11.
Idiom
Cluster Heatmaps
What: Derived T wo cluster hierarchies for table rows and columns.
How: Encode Heatmap: 2D matrix alignment, ordered by both
cluster hierarchies. Dendrogram: connection linemarks for parent–child relationships in tree.
Example: Scatterplot Matrix
Ascatterplot matrix (SPLOM) is a matrix where each cell contains an en-
tire scatterplot chart. A SPLOM shows all possible pairwise combinationsof attributes, with the original attributes as the rows and columns. Fig-ure 15.2 shows an example. In contrast to the simple heatmap matrixwhere each cell shows one attribute value, a SPLOM is an example of amore complex matrix where each cell shows a complete chart.
/trianglerightsldSPLOMS are an example
of small-multiple views, as
discussed in Section 12.3.2.
The key is a simple derived attribute that is the same for both the rows
and the columns: an index listing all the attributes in the original dataset.
The matrix could be reordered according to any ordered attribute. Usually7.5. Separate, Order, and Align: Categorical Regions 161
only the lower or upper triangle of the matrix is shown, rather than the
redundant full square. The diagonal cells are also typically omitted, sincethey would show the degenerate case of an attribute plotted against itself,so often labels for the axes are shown in those cells.
SPLOMs are heavily used for the abstract tasks of ﬁnding correlations,
trends, and outliers, in keeping with the usage of their constituent scat-terplot components.
Each scatterplot cell in the matrix requires enough room to plot a dot
for each item discernably, so around 100 ×100 pixels is a rough lower
bound. The scalability of a scatterplot matrix is thus limited to aroundone dozen attributes and hundreds of items./trianglerightsld Many extensions to
SPLOMs have been pro-
posed, including the scag-nostics idiom using derivedattributes described in Sec-tion 15.3 and the compactheatmap-style overviewdescribed in Section 15.5.
Idiom
Scatterplot Matrix (SPLOM)
What: Data Ta bl e.
What: Derived Ordered key attribute: list of original attributes.
How: Encode Scatterplots in 2D matrix alignment.
Why: T ask Find correlation, trends, outliers.
Scale Attributes: one dozen.
Items: dozens to hundreds.
7.5.3 Volumetric Grid: Three Keys
Just as data can be aligned in a 1D list or a 2D matrix, it is pos-
sible to align data in three dimensions, in a 3D volumetric grid.However, this design choice is typically not recommended for non-spatial data because it introduces many perceptual problems, in-cluding occlusion and perspective distortion. An alternative choice/trianglerightsldThe rationale for avoid-
ing the unjustiﬁed use of 3D
for nonspatial data is dis-cussed in Section 6.3.
for spatial layout for multidimensional tables with three keys is
recursive subdivision, as discussed below.
7.5.4 Recursive Subdivision: Multiple Keys
With multiple keys, it’s possible to extend the above approachesby recursively subdividing the cell within a list or matrix. That is,ordering and alignment is still used in the same way, and contain-ment is added to the mix.
There are many possibilities of how to partition data into sepa-
rate regions when dealing with multiple keys. These design choicesare discussed in depth in Section 12.4.162 7. Arrange T ables
7.6 Spatial Axis Orientation
An additional design choice with the use of space is how to ori-
ent the spatial axes: whether to use rectilinear, parallel, or radiallayout.
7.6.1 Rectilinear Layouts
In a rectilinear layout, regions or items are distributed along two
perpendicular axes, horizontal and vertical spatial position, thatrange from minimum value on one side of the axis to a maximumvalue on the other side. Rectilinear layouts are heavily used in visdesign and occur in many common statistical charts. All of theexamples above use rectilinear layouts.
7.6.2 Parallel Layouts
The rectilinear approach of a scatterplot, where items are plottedas dots with respect to perpendicular axes, is only usable for twodata attributes when high-precision planar spatial position is used.Even if the low-precision visual channel of a third spatial dimen-sion is used, then only three data attributes can be shown usingspatial position channels. Although additional nonspatial chan-
/trianglerightsldThe potential drawbacks
of using three spatial di-
mensions for abstract data
are discussed in Section 6.3.
nels can be used for visual encoding, the problem of channel in-
separability limits the number of channels that can be combinedeffectively in a single view. Of course, many tables contain far more/trianglerightsldThe issue of separable
versus integral channels is
covered in Section 5.5.3. than three quantitative attributes.
Example: Parallel Coordinates
The idiom of parallel coordinates is an approach for visualizing many quan-
titative attributes at once using spatial position. As the name suggests,
the axes are placed parallel to each other, rather than perpendicularly atright angles. While an item is shown with a dot in a scatterplot, with par-allel coordinates a single item is represented by a jagged line that zigzagsthrough the parallel axes, crossing each axis exactly once at the location ofthe item’s value for the associated attribute.
⋆Figure 7.12 shows an exam- ⋆In graphics terminology,
the jagged line is a poly-
line: a connected set of
straight line segments.ple of the same small data table shown both as a SPLOM and with parallelcoordinates.
One original motivation by the designers of parallel coordinates was
that they can be used for the abstract task of checking for correlation be-tween attributes. In scatterplots, the visual pattern showing correlationis the tightness of the diagonal pattern formed by the item dots, tilting7.6. Spatial Axis Orientation 163
Math
Physics
Dance
Drama
Math Physics Dance DramaMath Physics Dance Drama
100
90
80
70
6050 
40
30
20
10
0     Math Physics Dance Drama
85
9065
50
40958050
40
60706090
95
80655090
80
90Table Scatterplot Matrix Parallel Coordinates
Figure 7.12. Comparison of scatterplot matrix and parallel coordinate idioms for a small data table. After [McGuf-
ﬁn 14].
upward for positive correlation and downward for negative correlation.
If the attributes are not correlated, the points fall throughout the two-dimensional region rather than tightly along the diagonal. With parallelcoordinates, correlation is also visible, but through different kinds of vi-sual patterns, as illustrated in Figure 7.13. If two neighboring axes havehigh positive correlation, the line segments are mostly parallel. If two axeshave high negative correlation, the line segments mostly cross over eachother at a single spot between the axes. The pattern in between uncorre-lated axes is a mix of crossing angles.
However, in practice, SPLOMs are typically easier to use for the task
of ﬁnding correlation. Parallel coordinates are more often used for othertasks, including overview over all attributes, ﬁnding the range of individualattributes, selecting a range of items, and outlier detection. For example,in Figure 7.14(a), the third axis, labeled manu
wrkrs , has a broad range
nearly to the normalized limits of 628.50 and 441.50 , whereas the range of
values on the sixth axis, labeled cleared , is more narrow; the top item on
the fourth axis, labeled handgun lc, appears to be an outlier with respect
to that attribute.
Parallel coordinates visually encode data using two dimensions of spa-
tial position. Of course, any individual axis requires only one spatial di-
mension, but the second dimension is used to lay out multiple axes. The
scalability is high in terms of the number of quantitative attribute val-
ues that can be discriminated, since the high-precision channel of planarspatial position is used. The exact number is roughly proportional to thescreen space extent of the axes, in pixels. The scalability is moderate in164 7. Arrange T ables
Figure 7.13. Parallel coordinates were designed to show correlation between
neighboring axes. At the top, parallel lines show perfect positive correlation. At
the bottom, all of the lines cross over each other at a single spot in between thetwo axes, showing perfect negative correlation. In the middle, the mix of crossingsshows uncorrelated data. From [Wegman 90, Figure 3].
terms of number of attributes that can be displayed: dozens is common.
As the number of attributes shown increases, so does the width requiredto display them, so a parallel coordinates display showing many attributesis typically a wide and ﬂat rectangle. Assuming that the axes are vertical,then the amount of vertical screen space required to distinguish position
along them does not change, but the amount of horizontal screen space
increases as more axes are added. One limit is that there must be enoughroom between the axes to discern the patterns of intersection or paral-lelism of the line segments that pass between them.
The basic parallel coordinates idiom scales to showing hundreds of
items, but not thousands. If too many lines are overplotted, the resultingocclusion yields very little information. Figure 7.14 contrasts the idiomused successfully with 13 items and 7 attributes, as in Figure 7.14(a),versus ineffectively with over 16,000 items and 5 attributes, as in Fig-ure 7.14(b). In the latter case, only the minimum and maximum valuesalong each axis can be read; it is nearly impossible to see trends, anoma-lies, or correlations.
/trianglerightsldSection 13.4.1 covers
scaling to larger datasets
with hierarchical parallel co-ordinates.
The patterns made easily visible by parallel coordinates have to do
with the pairwise relationships between neighboring axes. Thus, the cru-7.6. Spatial Axis Orientation 165
(a)
 (b)
Figure 7.14. Parallel coordinates scale to dozens of attributes and hundreds of items, but not to thousands of items.
(a) Effective use with 13 items and 7 attributes. (b) Ineffective use with over 16,000 items and 5 attributes. From [Fua
et al. 99, Figures 1 and 2].
cial limitation of parallel coordinates is how to determine the order of the
axes. Most implementations allow the user to interactively reorder theaxes. However, exploring all possible conﬁgurations of axes through sys-tematic manual interaction would be prohibitively time consuming as thenumber of axes grows, because of the exploding number of possible com-binations.
Another limitation of parallel coordinates is training time; ﬁrst-time
users do not have intuitions about the meaning of the patterns they see,which must thus be taught explicitly. Parallel coordinates are often usedin one of several multiple views showing different visual encodings of thesame dataset, rather than as the only encoding. The combination of more
/trianglerightsld Multiple view design
choices are discussed in
Sections 12.3 and 12.4.familiar views such as scatterplots with a parallel coordinates view accel-
erates learning, particularly since linked highlighting reinforces the map-ping between the dots in the scatterplots and the jagged lines in the par-allel coordinates view.166 7. Arrange T ables
Idiom Parallel Coordinates
What: Data T able: many value attributes.
How: Encode Parallel layout: horizontal spatial position used to
separate axes, vertical spatial position used to ex-press value along each aligned axis with connectionline marks as segments between them.
Why: T asks Find trends, outliers, extremes, correlation.
Scale Attributes: dozens along secondary axis.
Items: hundreds.
7.6.3 Radial Layouts
In a radial spatial layout, items are distributed around a circle
using the angle channel in addition to one or more linear spatial
channels, in contrast to the rectilinear layouts that use only twospatial channels.
The natural coordinate system in radial layouts is polar coor-
dinates , where one dimension is measured as an angle from a
starting line and the other is measured as a distance from a cen-ter point. Figure 7.15 compares polar coordinates, as shown inFigure 7.15(a), with standard rectilinear coordinates, as shown inFigure 7.15(b). From a strictly mathematical point of view, rec-tilinear and radial layouts are equivalent under a particular kindof transformation: a box bounded by two sets of parallel lines istransformed into a disc where one line is collapsed to a point atthe center and the other line wraps around to meet up with itself,as in Figure 7.15(c).
However, from a perceptual point of view, rectilinear and ra-
dial layouts are not equivalent at all. The change of visual chan-nel has two major consequences from visual encoding principlesalone. First, the angle channel is less accurately perceived than arectilinear spatial position channel. Second, the angle channel isinherently cyclic, because the start and end point are the same, asopposed to the inherently linear nature of a position channel.
⋆The ⋆ In mathematical lan-
guage, the angle channel is
nonmonotonic .expressiveness and effectiveness principles suggest some guide-
lines on the use of radial layouts. Radial layouts may be more ef-fective than rectilinear ones in showing the periodicity of patterns,but encoding nonperiodic data with the periodic channel of angle7.6. Spatial Axis Orientation 167
10
2
4
685
1234
(a)5
1234
10 24 6 8
(b) (c)
Figure 7.15. Layout coordinate systems. (a) Radial layouts use polar coordinates,
with one spatial position and one angle channel. (b) Rectlinear layouts use two
perpendicular spatial position channels. After [Wickham 10, Figure 8]. (c) T rans-forming rectilinear to radial layouts maps two parallel bounding lines to a point atthe center and a circle at the perimeter.
may be misleading. Radial layouts imply an asymmetry of impor-
tance between the two attributes and would be inappropriate whenthe two attributes have equal importance.
Example: Radial Bar Charts
The same ﬁve-attribute dataset is encoded with a rectilinear bar chart in
Figure 7.16(a) and with a radial alternative in Figure 7.16(b). In bothcases, line marks are used to encode a quantitative attribute with thelength channel, and the only difference is the radial versus the rectilinearorientation of the axes.
(a)
 (b)
Figure 7.16. Radial versus rectilinear layouts. (a) Rectilinear bar chart. (b) Radial
bar chart. After [Booshehrian et al. 11, Figure 4].168 7. Arrange T ables
Idiom Radial Bar Charts
What: Data T able: one quantitative attribute, one categorical at-
tribute.
How: Encode Length coding of line marks; radial layout.
Example: Pie Charts
The most commonly used radial statistical graphic is the pie chart, shownin Figure 7.17(a). Pie charts encode a single attribute with area marksand the angle channel. Despite their popularity, pie charts are clearlyproblematic when considered according to the visual channel propertiesdiscussed in Section 5.5. Angle judgements on area marks are less ac-curate than length judgements on line marks. The wedges vary in widthalong the radial axis, from narrow near the center to wide near the outside,
making the area judgement particularly difﬁcult. Figure 7.17(b) shows a
bar chart with the same data, where the perceptual judgement required toread the data is the high-accuracy position along a common scale channel.Figure 7.17(c) shows a third radial chart that is a more direct equivalent ofa bar chart transformed into polar coordinates. The polar area chart also
encodes a single quantitative attribute but varies the length of the wedgejust as a bar chart varies the length of the bar, rather than varying theangle as in a pie chart.
⋆The data in Figure 7.17 shows the clarity dis-⋆Synonyms for polar area
chart are rose plot and
coxcomb plot ; these were
ﬁrst popularized by Flo-
rence Nightingale in the
19th century in her analy-sis of Crimean war medicaldata.tribution of diamonds, where I1is worst and IFis best. These instances
redundantly encode each mark with color for easier legibility, but these
idioms could be used without color coding.
(a)
 (b)
 (c)
Figure 7.17. Pie chart versus bar chart accuracy. (a) Pie charts require angle and area judgements. (b) Bar charts
require only high-accuracy length judgements for individual items. (c) Polar area charts are a more direct equivalent
of bar charts, where the length of each wedge varies like the length of each bar. From [Wickham 10, Figures 15and 16].7.6. Spatial Axis Orientation 169
<5
5-13
14-17
18-24
25-4445-64≥65
(a)UTTXIDAZNVGAAKMSNMNECAOKSDCOKSWYNCARLAINILMNDEHISCMOVAIATNKYALWAMDNDOHWIORNJMTMIFLNYDCCTPAMAWVRINHMEVT0%10%20%30%40%50%60%70%80%90%100%
Under 5 Years5 to 13 Years14 to 17 Years18 to 24 Years25 to 44 Years45 to 64 Years65 Years and Over
(b)CATXNYFLILPAOHMIGANCNJVAWAAZMAINTNMOMDWIMNCOALSCLAKYOROKCTIAMSARKSUTNVNMWVNEIDMENHHIRIMTDESDAKNDVTDCWY0.05.0M10M15M20M25M30M35M
Population65 Years and Over
45 to 64 Years
25 to 44 Years
18 to 24 Years
14 to 17 Years
5 to 13 Years
Under 5 Years
(c)
Figure 7.18. Relative contributions of parts to a whole. (a) A single pie chart shows the relative contributions of
parts to a whole, such as percentages, using area judgements. (b) Each bar in a normalized stacked bar chart
also shows the relative contributions of parts to a whole, with a higher-accuracy length encoding. (c) A stacked barchart shows the absolute counts in each bar, in contrast to the percentages when each bar is normalized to thesame vertical length. From http:/ /bl.ocks.org/mbostock/3887235, http:/ /bl.ocks.org/mbostock/3886208, http:/ /bl.ocks.org/mbostock/3886394.
The most useful property of pie charts is that they show the relative
contribution of parts to a whole. The sum of the wedge angles must addup to the 360
◦of a full circle, matching normalized data such as percent-
ages where the parts must add up to 100%. However, this property isnot unique to pie charts; a single bar in a normalized stacked bar chartcan also be used to show this property with the more accurate channelof length judgements. A stacked bar chart uses a composite glyph made
of stacking multiple sub-bars of different colors on top of each other; anormalized stacked bar chart stretches each of these bars to the maximum
possible length, showing percentages rather than absolute counts. Only
the lowest sub-bar in a stacked bar chart is aligned with the others in
its category, allowing the very highest accuracy channel of position withrespect to a common frame to be used. The other sub-bars use unalignedposition, a channel that is less accurate than aligned position, but stillmore accurate than angle comparisons.
/trianglerightsld Stacked glyphs are
discussed further in Sec-
tion 7.5.1.
Figure 7.18 compares a single pie chart showing aggregate population
data for the entire United States to a normalized stacked bar chart and a
stacked bar chart for all 50 states. An entire pie chart corresponds to asingle bar in these charts; an equivalent display would be a list or matrixof pies.
Pie charts require somewhat more screen area than normalized stacked
bar charts because the angle channel is lower precision than the lengthchannel. The aspect ratio also differs, where a pie chart requires a square,whereas a bar chart requires a long and narrow rectangle. Both pie chartsand normalized stacked bar charts are limited to showing a small numberof categories, with a maximum of around a dozen categories.170 7. Arrange T ables
Idiom Pie Charts
What: Data T able: one quantitative attribute, one categorical at-
tribute.
Why: T ask Part–whole relationship.
How: Encode Area marks (wedges) with angle channel; radial lay-out.
Scale One dozen categories.
Idiom Polar Area Charts
What: Data T able: one quantitative attribute, one categorical at-
tribute.
Why: T ask Part–whole relationship.
How: Encode Area marks (wedges) with length channel; radial lay-out.
Scale One dozen categories.
Idiom Normalized Stacked Bar Charts
What: Data Multidimensional table: one quantitative value at-
tribute, two categorical key attributes.
What: Derived One quantitative value attribute (normalized versionof original attribute).
Why: T ask Part–whole relationship.
How: Encode Line marks with length channel; rectilinear layout.
Scale One dozen categories for stacked attribute. Severaldozen categories for axis attribute.
Figure 7.19 compares rectilinear and radial layouts for 12 iconic
time-series datasets: linear increasing, decreasing, shifted, single
peak, single dip, combined linear and nonlinear, seasonal trends
with different scales, and a combined linear and seasonal trend[Wickham et al. 12]. The rectilinear layouts in Figure 7.19(a) aremore effective at showing the differences between the linear andnonlinear trends, whereas the radial plots Figure 7.19(b) are moreeffective at showing cyclic patterns.
A ﬁrst empirical study on radial versus rectilinear grid layouts
by Diehl et al. focused on the abstract task of memorizing positions
of objects for a few seconds [Diehl et al. 10]. They compared perfor-mance in terms of accuracy and speed for rectilinear grids of rowsand columns versus radial grids of sectors and rows. (The studydid not investigate the effect of periodicity.) In general, rectilinear7.7. Spatial Layout Density 171
(a)
(b)
Figure 7.19. Glyphmaps. (a) Rectilinear layouts are more effective at showing
the differences between linear and nonlinear trends. (b) Radial layouts are more
effective at showing cyclic patterns. From [Wickham et al. 12, Figure 3].
layouts outperformed radial layouts: perception speed was faster,
and accuracy tended to be better. However, their results also sug-gest the use of radial layouts can be justiﬁed when one attribute ismore important than the other. In this case, the more importantattribute should be encoded in the sectors and the less importantattribute in the rings.
7.7 Spatial Layout Density
Another design choice with spatial visual encoding idioms is whethera layout is dense or sparse. A related, but not identical, choice iswhether a layout is space-ﬁlling.172 7. Arrange T ables
7.7.1 Dense
Adense layout uses small and densely packed marks to provide an
overview of as many items as possible with very high information
density.⋆A maximally dense layout has point marks that are only ⋆A synonym for dense is
pixel-oriented . a single pixel in size and line marks that are only a single pixel inwidth. The small size of the marks implies that only the planarposition and color channels can be used in visual encoding; size
and shape are not available, nor are others like tilt, curvature, orshape that require more room than is available.
Section 15.4 presents a detailed case study of VisDB, a dense
display for multidimensional tables using point marks.
Example: Dense Software Overviews
Figure 7.20 shows the Tarantula system, a software engineering tool for
visualizing test coverage [Jones et al. 02]. Dense displays using line markshave become popular for showing overviews of software source code. Inthese displays, the arrangement of the marks is dictated by the orderand length of the lines of code, and the coloring of the lines encodes anattribute of interest.
Most of the screen is devoted to a large and dense overview of source
code using one-pixel tall lines, color coded to show whether it passed,failed, or had mixed results when executing a suite of test cases. Al-though of course the code is illegible in the low-resolution overview, thisview does convey some information about the code structure. Indenta-
tion and line length are preserved, creating visible landmarks that help
orient the reader. The layout wraps around to create multiple horizontalcolumns out of a single long linear list. The small source code view inthe lower left corner is a detail view showing a few lines of source code ata legible size; that is, a high-resolution view with the same color codingand same spatial position. The dense display scales to around ten thou-sand lines of code, handling around one thousand vertical pixels and tencolumns.
The dataset used by Tarantula is an interesting complex combination
of the software source code, the test results, and derived data. The orig-inal dataset is the software source code itself. Software code is highlystructured text that is divided into numbered lines and has multiscale hi-erarchical structure with divisions into units such as packages, ﬁles, andmethods. Most complex tasks in the software engineering domain requirereading snippets of code line by line in the order that they were written bythe programmer as a subtask, so changing or ignoring the order of lineswithin a method would not be an appropriate transformation. However,it’s common with software engineering tasks that only a small number ofthe many units in a software project need to be read at any given time.7.7. Spatial Layout Density 173
Figure 7.20. T arantula shows a dense overview of source code with lines color coded by execution status of a
software test suite. From [Jones et al. 02, Figure 4].
The design choice of a dense overview to provide orientation and a detail
view where a small amount of text is shown legibly is thus reasonable./trianglerightsldThe overview and detail
choice for multiple views is
covered in Section 12.3.The original dataset also includes the tests, where each test has the
categorical attribute of test or fail and is associated with a set of speciﬁc
lines of the source code. Tarantula computes two derived quantitativeattributes that are encoded with hue and brightness. The brightness en-codes the percentage of coverage by the test cases, where dark lines rep-resent low coverage and bright ones are high coverage. The hue encodesthe relative percentage of passed versus failed tests.
This example shows a full system that uses multiple idioms, rather
than just a single idiom. For completeness, the what–why–how analy-sis instance includes material covered in later chapters, about the de-sign choices of how to facet into multiple windows and how to reduce theamount of data shown.174 7. Arrange T ables
Idiom Dense Software Overviews
What: Data T ext with numbered lines (source code, test results
log).
What: Derived T wo quantitative attributes (test execution results).
How: Encode Dense layout. Spatial position and line length fromtext ordering. Color channels of hue and brightness.
Why: T ask Locate faults, summarize results and coverage.
Scale Lines of text: ten thousand.
(How: Facet) Same encoding, same dataset, global overview withdetail showing subset of data, different resolutions,linking with color.
(How: Reduce) Detail: ﬁlter to local neighborhood of selection
7.7.2 Space-Filling
Aspace-ﬁlling layout has the property that it ﬁlls all available space
in the view, as the name implies. Any of the three geometric pos-
sibilties discussed above can be space-ﬁlling. Space-ﬁlling layoutstypically use area marks for items or containment marks for rela-tionships, rather than line or connection marks, or point marks.Examples of space-ﬁlling layouts using containment marks are thetreemaps in Figures 9.8 and 9.9(f) and the nested circle tree in Fig-ure 9.9(e). Examples of space-ﬁlling layouts using area marks andthe spatial position channels are the concentric circle tree in Fig-ure 9.9(d) and the icicle tree of Figure 9.9(b).
One advantage of space-ﬁlling approaches is that they maxi-
mize the amount of room available for color coding, increasing thechance that the colored region will be large enough to be perceptu-ally salient to the viewer. A related advantage is that the availablespace representing an item is often large enough to show a labelembedded within it, rather than needing more room off to the side.
In contrast, one disadvantage of space-ﬁlling views is that the
designer cannot make use of white space in the layout; that is,
empty space where there are no explicit visual elements. Manygraphic design guidelines pertain to the careful use of white spacefor many reasons, including readability, emphasis, relative impor-tance, and visual balance.7.8. Further Reading 175
Space-ﬁlling layouts typically strive to achieve high information
density. However, the property that a layout ﬁlls space is by no
means a guarantee that is using space efﬁciently. More techni-cally, the deﬁnition of space-ﬁlling is that the total area used bythe layout is equal to the total area available in the view. There aremany other possible metrics for analyzing the space efﬁciency of alayout. For instance, for trees, proposed metrics include the size ofthe smallest nodes and the area of labels on the nodes [McGufﬁnand Robert 10].
7.8 Further Reading
The Big Picture Many previous authors have proposed ways to cat-
egorize vis idioms. My framework was inﬂuenced by manyof them, including an early taxonomy of the infovis designspace [Card and Mackinlay 99] and tutorial on visual idioms[Keim 97], a book on the grammar of graphics [Wilkinson 05], ataxonomy of multidimensional multivariate vis [McGufﬁn 14],papers on generalized pair plots [Emerson et al. 12] and prod-uct plots [Wickham and Hofmann 11], and a recent taxon-omy [Heer and Shneiderman 12]. Bertin’s very early bookSemiology of Graphics has been a mother lode of inspiration
for the entire ﬁeld and remains thought provoking to thisday [Bertin 67].
History The rich history of visual representations of data, with par-
ticular attention to statistical graphics such as time-seriesline chart, the bar chart, the pie chart, and the circle chart,is documented at the extensive web site http:/ /www.datavis.ca/milestones [Friendly 08].
Statistical Graphics A book by statistician Bill Cleveland has an ex-
cellent and extensive discussion of the use of many tradi-tional statistical charts, including bar charts, line charts, dotcharts, and scatterplots [Cleveland 93b].
Stacked Charts The complex stacked charts idiom of streamgraphs
was popularized with the ThemeRiver system [Havre et al. 00];later work analyzes their geometry and asthetics in detail [By-ron and Wattenberg 08].
Bar Charts versus Line Charts A paper from the cognitive psychology
literature provides guidelines for when to use bar charts ver-sus line charts [Zacks and Tversky 99].176 7. Arrange T ables
Banking to 45 Degrees Early work proposed aspect ratio control by
banking to 45◦[Cleveland et al. 88,Cleveland 93b]; later work
extended this idea to an automatic multiscale framework [Heer
and Agrawala 06].
Heatmaps and Matrix Reordering One historical review covers the rich
history of heatmaps, cluster heatmaps, and matrix reorder-ing [Wilkinson and Friendly 09]; another covers matrix re-ordering and seriation [Liiv 10].
Parallel Coordinates Parallel coordinates were independently pro-
posed at the same time by a geometer [Inselberg and Dims-dale 90, Inselberg 09] and a statistician [Wegman 90].
Radial Layouts Radial layouts were characterized through empirical
user studies [Diehl et al. 10] and have also been surveyed
[Draper et al. 09].
Dense Layouts Dense layouts have been explored extensively for
many datatypes [Keim 00]. The SeeSoft system was an earlydense layout for text and source code [Eick et al. 92]; Taran-tula is a later system using that design choice [Jones et al. 02].