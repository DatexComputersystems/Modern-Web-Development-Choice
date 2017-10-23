# Modern-Web-Development-Choice
Scientific work of some decisions that need to be taken into account when rewriting an enterprise application with modern web technologies. Written by Mikey Stengel in the course of exam to Bachelor of Science (B. Sc.)

## **2nd project thesis In the course of exam to Bachelor of Science (B. Sc.)**

**University: DHBW Karlsruhe, faculty economy**

**Title: Rework of an obsolete desktop application code-base into a single-page application**

**Author: Mikey Stengel**

**Company: Datex Computersysteme GmbH**

**Scientific supervisor: Katja Wengler**

**Date: Karlsruhe, 05.09.2017**

# Table of contents

[List of illustrations](#listofillustrations)

[List of tables](#listoftables)

[List of attachments](#listofattachments)

[Typographical conventions](#typographicalconventions)

[Table of abbreviations](#tableofabbreviations)

1 [Introduction](#introduction)

&nbsp;&nbsp; 1.1 [Problem definition](#problemdefinition)

&nbsp;&nbsp; 1.2 [Structure](#structure)

&nbsp;&nbsp; 1.3 [Target audience](#targetaudience)

&nbsp;&nbsp; 1.4 [Objective](#objective)

2 [Fundamentals](#fundamentals)

&nbsp;&nbsp; 2.1 [Reimplementation](#reimplementation)

&nbsp;&nbsp; 2.2 [Amadeus](#amadeus)

&nbsp;&nbsp; 2.3 [Functional Programming](#functionalprogramming)

&nbsp;&nbsp; 2.4 [Scala](#scala)

&nbsp;&nbsp; 2.5 [Node.js](#nodejs)

&nbsp;&nbsp; 2.6 [Modern web development](#modernwebdevelopment)

&nbsp;&nbsp;&nbsp;&nbsp; 2.6.1 [Single Page Application](#singlepageapplication)

&nbsp;&nbsp;&nbsp;&nbsp; 2.6.2 [Ambitious Web Application](#ambitiouswebapplication)

&nbsp;&nbsp;&nbsp;&nbsp; 2.6.3 [Progressive Web Application](#progressivewebapplication)

&nbsp;&nbsp; 2.7 [React.js](#reactjs)

&nbsp;&nbsp; 2.8 [Ember.js](#emberjs)

3 [Requirements analysis](#requirementsanalysis)

4 [Evaluation of technologies](#evaluationoftechnologies)

&nbsp;&nbsp; 4.1 [Front end](#frontend)

&nbsp;&nbsp;&nbsp;&nbsp; 4.1.1 [Learn](#frontendlearn)

&nbsp;&nbsp;&nbsp;&nbsp; 4.1.2 [CLI](#frontendcli)

&nbsp;&nbsp;&nbsp;&nbsp; 4.1.3 [Development](#frontenddevelopment)

&nbsp;&nbsp;&nbsp;&nbsp; 4.1.4 [Test, Build, Deploy](#frontendtestbuilddeploy)

&nbsp;&nbsp;&nbsp;&nbsp; 4.1.5 [Scale, Performance, Maintain](#frontendscaleperformancemaintain)

&nbsp;&nbsp;&nbsp;&nbsp; 4.1.6 [Package size](#frontendpackagesize)

&nbsp;&nbsp;&nbsp;&nbsp; 4.1.7 [Decision](#frontenddecision)

&nbsp;&nbsp; 4.2 [Back end](#backend)

&nbsp;&nbsp;&nbsp;&nbsp; 4.2.1 [Learn](#backendlearn)

&nbsp;&nbsp;&nbsp;&nbsp; 4.2.2 [Development](#backenddevelopment)

&nbsp;&nbsp;&nbsp;&nbsp; 4.2.3 [Test, Secure, Build, Deploy](#backendtestsecurebuilddeploy)

&nbsp;&nbsp;&nbsp;&nbsp; 4.2.4 [Maintain](#backendmaintain)

&nbsp;&nbsp;&nbsp;&nbsp; 4.2.5 [Scale](#backendscale)

&nbsp;&nbsp;&nbsp;&nbsp; 4.2.6 [Decision](#backenddecision)

5 [Migration path](#migrationpath)

6 [Conclusion](#conclusion)

[Glossary](#glossary)

[Attachments](#attachments)

[References](#references)

<a name="listofillustrations"></a>

# List of illustrations

[1. Figure – Performance: create 10.000 rows](#firstfigure)

[2. Figure – Performance: update every 10th row](#secondfigure)

[3. Figure – Migration phase #1: Rewrite of Amadeus &amp; Starserver migration](#thirdfigure)

[4. Figure – Migration phase #2: Rewrite of Amadeus &amp; adding features](#forthfigure)

[5. Figure – Migration phase #3: Progressive, ambitious web application](#fifthfigure)

<a name="listoftables"></a>

# List of tables

[1. Table – Front end: Selection criteria with description](#firsttable)

[2. Table – Front end: Decision matrix](#secondtable)

[3. Table – Front end: GitHub comparison](#thirdtable)

[4. Table – Back end: Selection criteria with description](#forthtable)

[5. Table – Back end: GitHub comparison](#fifthtable)

[6. Table – Back end: Decision matrix](#sixthtable)

<a name="listofattachments"></a>
# List of attachments 

[1. Attachment – Market share operating systems](#firstattachment)

[2. Attachment – React and Ember ecosystem](#secondattachment)

[3. Attachment – Back-end performance](#thirdattachment)

[4. Attachment – Latency comparison](#forthattachment)

<a name="typographicalconventions"></a>
# Typographical conventions 

Following typographical conventions are used throughout the study.

**List of abbreviations**

The list of abbreviations contains an alphabetically sorted list with all the abbreviations that are being utilized in the following project thesis. Abbreviations will only be used after the full form of the words have been written out at least once in the text to enhance readability. They will also be reflected in the abbreviation list.

**Glossary**

At the end of the paper, there is an alphabetically sorted glossary with explanations to certain keywords. In favor of readability, words which require an explanation are marked with the following sign: &#9998;. Immediate clarified terms in the text are not listed in the keyword index anew.

**References**

Sources are referenced in parenthesis after their respective paragraph or sentence. Incremental footnotes in the text point to footers, which contain additional information. An alphabetically sorted list of all the used literature, which is referenced by the inline parenthesis, can be found in the bibliography at the end of this paper.

**Adjuncts**

A CD with an electronic version of this project thesis, and the source code that was being used is attached to the printed work

**Other**

In favor of consistency, &#39;Node.js&#39; is treated as a server-side language, while technically being a server-side technology. Further, the terms future- or futuristic Amadeus always refer to the new implementation of Amadeus and are used interchangeably.

<a name="tableofabbreviations"></a>
# Table of abbreviations 

|  |  |
| --- | --- |
| Component Object Model | COM |
| Document Object Model | DOM |
| Dynamic Link Library | DLL |
| Generic Java | GJ |
| graphical user interface | GUI |
| Hypertext Markup Language | HTML |
| integrated development environment | IDE |
| input/output | I/O |
| Java Virtual Machine | JVM |
| Model View Controller | MVC |
| Remote Method Invocation | RMI |
| Representational State Transfer | REST |
| single-page application | SPA |
| user interface | UI |
| Visual Basic 6 | VB6 |
| XMLHttpRequest | XHR |

<a name="introduction"></a>
# 1. Introduction 

<a name="problemdefinition"></a>
## 1.1 Problem definition 

Datex Computersysteme GmbH develops real estate software since nearly three decades. The primary product – Amadeus, which is a commercial industry-specific software for real estate developer – has been around for almost as long and enriched the productivity and workflow of thousands of customers to this day. As of now, Amadeus is almost entirely written in Visual Basic 6 (VB6) &#9998;. Unfortunately, the support for Visual Basic Classic &#9998;, the integrated development environment (IDE) and many libraries ended a long time ago. (Yuknewicz, Latham, Onderka, &amp; Petrusha, 2016) This means that the current development process is tedious, slow and error-prone as modern quality management tools can&#39;t be used with ease. Finally, Datex decided to rewrite Amadeus with modern languages from scratch.

A look at the history of programming languages show how quickly the industry changes and how most languages behave like the classic economic product life cycle. A new language is introduced, grows and peeks until it finally declines, where it will in most cases be used by only a few companies or ditched entirely by its respective community for a more innovative language; hence when selecting a new programming language, many different parameters must be considered and evaluated. With contemporary technologies emerging daily as well as an ever-changing industry, choosing the correct language has never been more challenging.

Considering that not only the language but also the codebase, database and underlying technologies of Amadeus are mostly obsolete, Datex developers can not only change the language in use, but also make use of disruptive innovation &#9998; to reimplement the underlying logic and create a new futuristic Amadeus that is built on best practices across the modern development era.

Since the current version of Amadeus must be maintained while we work on the rewrite, establishing a resource-saving migration path that allows improvements of the current software without losing the resources spend to do so, is essential.

<a name="structure"></a>
## 1.2 Structure 

Present paper will evaluate existing and new bleeding edge technologies &#9998; in various aspects, compare them and consequential articulate recommendations about what technologies suit Amadeus in the best viable way, based on scientific evidence.

To start off, the fundamentals chapter will describe our software to give precise information about what it is capable of and the customers that use Amadeus daily. The technologies that are reviewed more in depth, than others, can also be found inside of the fundamentals chapter. This is meant to help comprehend some technical aspects and characteristics of the technologies, which are needed for later chapters.

Afterwards, the requirements analysis will showcase what kind of problems need to be solved by changing technologies. Eventually, decision criteria for the comparison will be derived from the requirements analysis and evaluated carefully.

The central part of the present scientific work is the evaluation and comparison of different technologies. Switching to modern technologies will expose long-term advantages compared to the current development stack. The technologies that will be assessed include and prioritize, but are not limited to, the comparison of languages. Similarly, certain frameworks, libraries and tools – primarily created by the open source community – will also be broadly compared to their respective competing counterparts. The end of each comparison chapter should advocate the use of certain technologies based on empirical, scientific evidence.

Finally, several action recommendations from previous chapters should enable Datex with new possibilities to write sophisticated software and the application area of the new development stack will be concluded. Additionally, a migration path will be proposed and a broad prospect of future development evaluates the longevity of the proposed technologies.

<a name="targetaudience"></a>
## 1.3 Target audience 

The scientific work is targeted towards any developer that must assess different technologies and will showcase scientific methods that help to make decisions based on empirical evidence. As an aside, the results will be Amadeus specific and undoubtedly differ from case to case, whereas the evaluation process and decision-making method will be similar for everyone.

<a name="objective"></a>
## 1.4 Objective 

Since most online resources that compare different languages, tools or framework are non-scientific and statistics do not always represent the reality, the following paper tries to provide impartial methods to evaluate and compare similar, competing technologies to each other. Consequently, the main goal of the project thesis is to assess different technologies from different angles and compare them in a non-biased way to conclude which language, tool or framework suits the rewrite of Amadeus in the best feasible way to not only enhance quality standards and embrace best practices, but also to increase productivity amongst the developers. The center of the project thesis is to establish a well-maintained development stack that enables the usage of modern development tools and most importantly, rewrite Amadeus in a cost-efficient manner. At the same time, maintaining the current version of Amadeus midst the development of the futuristic Amadeus is also of high priority.

The paper is also meant to give developers a broad overview of some of the technologies that exist to resolve certain problems so that individuals can make decisions for their respective use case.

Rewriting Amadeus is not part of the scientific work, as it would go beyond the scope of this thesis.

<a name="fundamentals"></a>
# 2. Fundamentals 

<a name="reimplementation"></a>
## 2.1 Reimplementation 

The reimplementation paradigm can be realized by first analyzing the system using a method called architecture reconstruction &#9998;. After a certain task or user story within the system has been identified and detached from the specific programming language (Pugh, 2005, p. 160), one can start reimplementing the problem in any target language based on the understanding of the problem. (Waters, 1988) Detachment from the current architecture and language is not only important to prevent the disadvantageous copy pasting of tasks (Maurer &amp; Kulathuramaiyer, 2007) into a newer system but also to reason through the first-principle school of thought (Yourgrau &amp; Beginnen, 2005, 197f), which enables developers to think about certain problems anew, ultimately improving the solution in the process. If this process is repeated for each subproblem within a software system, the program can be considered reimplemented.

<a name="amadeus"></a>
## 2.2 Amadeus 

Amadeus is a commercial software for real estate owner, project leader and other businessperson in the real estate development market. Initially released in 1991, it went through a lot of changes in its early days.

In 1993 developers of Datex decided to rewrite Amadeus in Visual Basic 3, leaving the programming language &#39;Clipper&#39; as well as its respective database &#39;dBase&#39; behind. Ever since the change, Amadeus uses Microsoft&#39;s access database as well as the newest version of Visual Basic Classic, whose support ended shortly after the sixth version with the introduction to the .NET framework. Microsoft stated repeatedly that they won&#39;t open source nor bring back the old Visual Basic. (Yuknewicz, 2014) Over the years, Datex used interoperability of the Component Object Model (COM) &#9998; to make use of some .NET features while still having most of the code-base written in an obsolete language. The languages restrict Amadeus on both the server-, as well as the client side, to only run on an underlying Windows operating system. Amadeus enables real estate developers to be more productive and to have an easier time maintaining projects, to publish them to a variety of different real estate portals and to handle financial accounting. As Amadeus matures, it has changed a lot; the current version (IX) has been in development for nearly 13 years and brought a variety of changes to functionality, the graphical user interface (GUI) and most importantly code quality. After the release of the latest version, Amadeus supports two databases. Access and PostgreSQL both need to be maintained in the future.

<a name="functionalprogramming"></a>
## 2.3 Functional Programming 

Functional Programming is a programming paradigm that is based on the premise to create projects from solely pure functions. (Chiusano &amp; Bjarnason, 2015, 3f) Pure functions do not have any side effects due to referential transparency, which makes pure functions predictive, and consists out of several properties such as extensionality, definiteness, and unfoldability. (Ram; Sndergaard &amp; Sestoft, 1990, 505f) Since pure functions always have a precisely defined purpose, they are easier to understand and reason about. (Chiusano &amp; Bjarnason, 2015, p. 9) The result of having no side effects is that those functions are easier to maintain in terms of debugging and testing.

Other notable functional programming concepts include first class functions to allow passing functions as arguments (Chiusano &amp; Bjarnason, 2015, p. 14; Odersky, Spoon, &amp; Venners, 2010) and pattern matching, which &quot;works a bit like a fancy switch statement that may descend into the structure of the expression it examines and extract subexpressions of that structure.&quot; (Chiusano &amp; Bjarnason, 2015, 32f)

Functional programming influenced many other languages throughout its long history, going back to lambda calculus in the 1930s. Ever since an international research committee introduced Haskell with the intention to fully standardize a lazy, functional language (Meijer, 2009, 8:20–17:00), &quot;functional programming seemed on an upward trajectory, out of academia into &#39;real-world&#39; computing.&quot; (Michaelson, 2011, iii)

Functional languages that don&#39;t produce side-effects at all are called purely functional programming languages, while others that contain or allow code with side effects are called impure languages. (SABRY, 1998, p. 1)

<a name="scala"></a>
## 2.4 Scala 

Scala is an impure functional, object-oriented, imperative programming language. German scientist Martin Odersky initially took some functional programming aspects in conjunction with Java and created the Pizza programming language, followed by Generic Java (GJ). Even though the languages supported higher order functions, pattern matching, and generics, he wanted to take it a step further and rewrote Java almost entirely, except for the underlying Java Virtual Machine (JVM) &#9998; architecture. Scala was the result of GJ and &#39;Funnel&#39;, an academic prototype of Scala, released in 2003 (Venners &amp; Sommers, 2009) and stands for &#39;scalable language&#39;. It works with all Java libraries, thus enabling developers to access a huge ecosystem of frameworks, tools, and libraries. (Odersky et al., 2010, p. 3)

Neal Gafter describes Scala in his foreword to &#39;Programming in Scala&#39; as &quot;tastefully typed language&quot; (Odersky et al., 2010, xxxix) because it is statically typed &#9998;, but can be explicitly typed &#9998; in places necessary. This somewhat flexible behavior can be seen throughout the whole language specification (Odersky, 2014, p. 183) and always tries to combine the best of both, functional and object-oriented, worlds. Both, pure and impure functions are supported, but it is generally advised to stick to pure functions. (Chiusano &amp; Bjarnason, 2015, xiii)

<a name="nodejs"></a>
## 2.5 Node.js 

JavaScript is a highly flexible language that was originally known for running in the browser. When Google open sourced their JavaScript engine – V8 – in 2008, the essentials to a rich ecosystem were set, and it didn&#39;t take long until the community made use of it. (McCune, 2011, 1f) At the end of 2009, the 5th edition of the ECMAScript &#9998; standard was released by the TC39 consortium &#9998;, resulting in even more JavaScript publicity and developers working on it. At the same time, Ryan Dahl saw the flexibility and event loop &#9998; of JavaScript as a huge advantage and started working on Node.js to overcome some problems of other languages. When he released Node.js, JavaScript could be written on the server. (Springer, 2013, 21f) Node.js was built with the premise to fix blocking input/output (I/O) and that &quot;threaded concurrency is a leaky abstraction&quot; (Dahl, 2009, 7:00–8:00). Thus, it is built on V8 and uses the event loop to allow asynchronous non-blocking I/O, running in a single thread. (Jensen, 2017, p. 92) Node.js also makes use of many C and C++ libraries to allow functionality through modules like streaming, sockets and I/O. An ever-growing open source community and the addition of a package manager that allows easy package distribution (Debill; Välimäki, 2005, p. 17) in 2010 (Schlueter, 2010), lead to even more popularity and Node.js being adopted by large companies. Node.js provides the fundamentals and underlying, platform independent architecture for many great technologies. (Cravens &amp; Brady, 2014, p. 9) Under those circumstances, Electron.js &#9998; use Node.js to concede the possibility of creating cross-platform desktop applications using JavaScript. (Jensen, 2017, p. 115)

<a name="modernwebdevelopment"></a>
## 2.6 Modern web development 

Web development has changed a lot over the past couple of years. To verbally describe new possibilities, new vocabulary was mandatory. The obsolete term web page indicates static, non-dynamic content; Whereas, modern technologies allow developers to create feature-rich, highly interactive, dynamic and fast web applications. Following chapters explain the vocabulary that will be used throughout the book.

<a name="singlepageapplication"></a>
### 2.6.1 Single Page Application 

The developer community had developed web pages that refreshed with every user action for years, before XMLHttpRequest (XHR) was introduced. The possibility of &quot;inner-browsing&quot; lead to the opportunity to have fully functional web applications within a single page. (Galli &amp; Perrier, 2003; van Kesteren, 2017) Advancing technologies provide functionality such as Document Object Model (DOM) &#9998; manipulation, routing and XHR to build Single Page Applications (SPA).

<a name="ambitiouswebapplication"></a>
### 2.6.2 Ambitious Web Application 

Ambitious Web Application is a broad term firstly introduced by the Ember.js community to describe the range of possibilities using their framework. The baseline is that HTTP – the fundament of the World Wide Web – is stateless, while modern web applications have an obligation to be stateful. Furthermore, it takes the original idea behind SPAs, to provide a native desktop application feel, even further to create a better user experience. (Cravens &amp; Brady, 2014, pp. 1–5; Katz, 2013, 0:45-15:00)

<a name="progressivewebapplication"></a>
### 2.6.3 Progressive Web Application 

Progressive Web Apps target mainly mobile clients and support many functionalities that are usually associated with native apps, viz. offline- or instant loading, push notifications and responsiveness. (Zolciak, 2017)

<a name="reactjs"></a>
## 2.7 React.js 

React is a front-end library to create graphical user interfaces. After being originally developed by Facebook in 2011, they open-sourced it in May 2013 by releasing their code to GitHub. Nowadays, the community and dedicated Facebook developer maintain React and the adjacent ecosystem.

The premise of the modern technology comes back to what Douglas Crockford, a JavaScript author and developer, has preached for years: &quot;The reason the browser is so awful is not because of JavaScript, it is because of the DOM.&quot; (Crockford, 2009, 4:40) In other words, the DOM is too slow and as a consequence modern applications have to make use of as much JavaScript as possible. React makes use of a virtual DOM. Any state changes in the application affect the virtual DOM and a heuristic difference algorithm called &#39;Reconciliation&#39; compares both trees to each other and only renders exactly the parts that changed. (Lacker, 2016b; Banks &amp; Porcello, 2017, 61f; Abramov, 2015a) React provides a declarative API to render DOM elements and is mostly considered as the &#39;V&#39; in the Model View Controller (MVC) &#9998; architecture. React components are building blocks of web applications and are usually declared through the JSX &#9998; programming language. The declarative approach also makes use of many functional programming paradigms such as stateless functional (pure) components, higher order components and immutability. (Banks &amp; Porcello, 2017, 40f; 73; 166)

The rendering engine and core algorithm of React is called Fiber and was a complete rewrite of React. (Dodds, Abramov, &amp; Clark, 2016, 2:45–57:20; Clark, 2017, 0:25)

<a name="emberjs"></a>
## 2.8 Ember.js 

Ember.js is an open-source front end MVC JavaScript framework to create single-page applications. In 2011, SproutCore – another JavaScript framework – 2.0 was rebranded as Ember.js. (Scheffler, 2017) Due to the fact, that it was one of the earliest JavaScript frameworks to implement routing and other features that are now considered standard for every major front-end library (Katz, 2013, 16:40–18:00), Ember has been a role model for many technologies over the past couple of years.

Ember adopted a popular concept in the developer community called &#39;convention over configuration&#39;. As a result, every pattern, that is common enough becomes the default and doesn&#39;t have to be manually configured by the developer. (Cravens &amp; Brady, 2014, 7f)

Ember uses a templating engine called Handlebars (Decker, Katz, Johnson, &amp; Knappmeier, 2010) – a superset of Mustache.js (Lehnardt, Jackson, Silva, Cherry, &amp; Johnsen, 2009) – to write Hypertext Markup Language (HTML) in conjunction with JavaScript properties.

As a rendering engine Ember depends on Glimmer (Katz et al., 2013), which can also be used as a standalone module. Glimmer supports the immutable pattern (Dale, 2017a) and is written in TypeScript, a superset of JavaScript that guarantees type safety.

With the intention to be an opinionated framework with as little manual configurations as possible, Ember supports a rich ecosystem of add-ons, which can be added or removed via npm or the Ember-CLI. (Burgess, 2017, 2ff; Penner et al., 2013)

<a name="requirementsanalysis"></a>
# 3. Requirements analysis 

Ever since the start of modern computing, constant hardware improvements made computers accessible to most of the mankind. A bigger community lead to more disruptive innovations, repeatedly pushing obsolete technology from the developer market. Many technologies, languages, best practices and the consensus of how things should be done changed over the past decades dramatically. In every regard, there are more options a developer can choose today, than ever before. It has never been more important, to carefully examine the underlying problem of a system and evaluate all the options. Agile development allows a more dynamic and flexible development, but does not simplify the process of concluding key prerequisites. The requirements analysis focuses on the problems Datex hopes to solve by moving to entirely modern technologies; Furthermore, it also tries to limit the scope of possibilities to choose from, by defining the expected outcome of this thesis and the resulting selection criteria.

Currently Amadeus runs only on Windows servers and Windows clients. The market share of all non-windows systems for desktop devices was accumulated to around 9.5% in 2016 (Att. 1 – Market share operating systems). If we assume that Datex currently has 10.000 customers that paid an average of 1.250€ for the Amadeus license in conjunction with extra modules, Datex would miss out on 950 potential clients who create an economic value of 1.187.500€. This broad economic analysis alone showcases the commercial advantages of being independent of underlying operating systems.

An ever-growing Amadeus code base lead to a decreasing maintainability. How much Amadeus has changed regarding functionality and code is reflected in the user manuals and code dimensions. The user manual of the sixth Amadeus version had 266 pages in 2001. Since then, the manual has been growing to fivefold its volume to far above thousand pages. At the time of the sixth Amadeus version, the code base had roughly 200.000 lines of code separated into 178 form files. 0 classes were used at the time and when the management of Datex changed in 2003, they were inheriting a horrible code structure and had to refactor a lot of code in the following years. The decision to rather refactor Amadeus than to rewrite it from scratch was influenced by a lack of knowledge about Amadeus and time constraints. The current (Data from 16.05.2017) Amadeus code base contains 1.000.160 lines of code across 948 classes, 221 form files, and 33 projects. The documentation of Amadeus is limited to 37 different text files, a changelog with several thousand lines and comments in the code, which by now, are mostly deprecated. In recent years, some crucial Amadeus code was moved to Microsoft&#39;s .NET platform. The communication between VB6 and .NET works through interoperability of the Component Object Model. Due to some restrictions to COM, migrating code to .NET takes a lot of time and adds additional problems to the already unstable code base of Amadeus. The number of dependencies on dynamic link libraries still grows, doubtlessly emerging in Dynamic Link Library (DLL) &#9998; hell (Pratschner, 2001) every time a new Amadeus version is about to be released or significant changes are made. Many workarounds had to be introduced to make the development process and deployment less tedious. Unfortunately, the Visual Basic application is still dependent on 38 DLLs and can&#39;t make proper use of testing and other quality management tools, which would increase not only productivity but also the quality of the software. Enterprise programs in the magnitude of Amadeus without automated tests require an immense amount of resources to test different behaviors manually.

Tom Occhino, a manager at Facebook, defined the term &#39;quality software&#39; as a reliable, high performance and enjoyable application, while emphasizing the development speed (Occhino, Hunt, &amp; Chen, 2014, 4:40) in the interest of creating a valuable feedback loop for customers. Concerning the quality of Amadeus and in favor of disruptive innovation, Datex decided that the migration process of Amadeus, to adopt incrementally .NET, is too error prone and slow. Instead, developers settled on a ground-up rewrite to tackle problems that can&#39;t be solved with the current technologies in use or would require too many resources. Subsequently, the long-term objective is to have a well-documented, quality software, written with modern technologies and languages, cross-platform compatibility and most importantly to establish a rapid, maintainable development process. Cross-platform compatibility with the least amount of resources spend can be achieved by writing a web application. Moreover, because all our customers have been working with the old desktop application for decades, we want to create a desktop application that supports several desktop operating systems.

In addition to the complete rework of Amadeus, the current obsolete version must also be updated regularly to fulfill requests of our customers and fix new occurring bugs. Inasmuch, Datex can&#39;t spend the developer resources to focus solely on the new Amadeus. When new features are added to the current Amadeus, the code would need to be written again in another language for the futuristic Amadeus. That being the case, forces Datex developers to adopt a migration path, which allows to not only achieve the obligation to provide updates within the current version but also to reuse every feature that gets added to the existent Amadeus, within the rewritten web application.

A few developers at Datex experimented with the web approach by creating a Craftmanportal in Ember.js and Scala. The Craftmanportal is supposed to be a module of Amadeus and was developed before Datex decided to rewrite Amadeus from scratch instead of the incremental .NET migration. Since then, some additional requirements such as the demand for a desktop application were added to the responsibilities of the prospective Amadeus. Many team meetings around the topic lead to the conclusion to not rush any decision and think all possibilities through before settling on a specific technology. Nonetheless, the resources that were spent to write the code must be considered when deciding on a particular technology.

Due to the limited scope of this thesis, developers of Datex reduced the number of technologies to a bare minimum. The scientific work will only focus on the closer selection and only list existing alternatives. Amadeus is a big I/O oriented program; Therefore, easy maintainability, usage of test driven development, rapid development and backwards compatibility between different versions were one of the key prerequisites of any decision.

<a name="evaluationoftechnologies"></a>
# 4 Evaluation of technologies 

Before comparing technologies to each other, it is important to choose a method, which helps to solve a multiple-criteria decision analysis problem. There are a variety of methods for decision-making, but the decision-making paradox states that different methods may lead to different results. Even though the methods might be scientific, the decision-making paradox cannot be discarded, ultimately encouraging the decision maker to find an appropriate scientific method, repeat the evaluation process with several different methods or, which should be done regardless, reflect the result of the selected method critically. In 1947 Herring outlined the importance of scientific methods in crucial decisions by proposing the general need for a &quot;social science technician&quot;, anyone who is trained to apply scientific methods to practical situations in the interest of finding solutions. (Collins &amp; Guetzkow, op. 1964, 2f)

For the sake of clarity and simplicity, the following paper mainly uses the decision-matrix method, also known as Pugh method. Internally, different evaluation technologies were used to reduce the number of possibilities to a bare minimum.

<a name="frontend"></a>
## 4.1 Front end 

To begin with, there were several frameworks suitable for the futuristic Amadeus. Vue.js, Angular, Ember, React and Polymer were compared beforehand. With Ember and React making the closer selection, some adjustments had to be made to compare the Ember framework with the user interface (UI) library React. Since Ember recently open sourced their virtual rendering machine Glimmer, it would be possible to compare Glimmer to React; However, because Amadeus is reliant on more than just the view, it is better to add additional techniques to React to facilitate an equal comparison of React and Ember. React is mainly used with either the Flux architecture (Shannessy et al., 2014) or a state container called Redux (Abramov et al., 2015). Even though Flux was also created by Facebook, the community is mainly using Redux as it &quot;preserves all the benefits of Flux and adds new benefits&quot; (Abramov, 2015b). Consequently, React + Redux and Ember will be compared to each other.

The following table shows the selection criterion and their respective description.

**1. Table – Front end: Sel
<a name="firsttable"></a>ection criteria with description**

| Selection criteria | Description |
| --- | --- |
| Learn | The effort to learn the technology. |
| Setup project without CLI | Using the respective technology without a command line tool. |
| Setup project with CLI | Using the respective technology with a command line tool. |
| Development | Community, template language, server rendering, ecosystem, IDE support. |
| Test | Testing tools. |
| Build | Build tools. |
| Deploy | The effort to push applications to production and deploy them. |
| Debug | Browser inspectors or other tools that help to debug. |
| Scale | Scalability of the application. |
| Performance | Performance of DOM interactions. |
| Package size | Minified &#9998; and gzipped &#9998; package size. |
| Maintain | Backwards compatibility &#9998;, longevity. |

Initially, developers of Datex defined the weight of each criteria inside of the decision matrix. Note that the weight might vary for different applications. Coming from a Visual Basic background, rapid development was one of the top priorities of Datex, hence the high weight in every criterion that enhances the development workflow. The second table is based on the weight of each selection criteria and rates the technologies based on each specification, from 1 (very bad) to 10 (very good), individually. The rating of each criteria is subjective but reasoned through scientific methods, empirical evidence and conducted by internal Ember and React developers with extensive experience.

<a name="secondtable"></a>
**2. Table – Front end: Decision matrix**

| Selection criteria | Weight | Ember | React + Redux |
| --- | --- | --- | --- |
| Learn | 10 | 8 | 3 |
| Setup project without CLI | 1 | 5 | 1 |
| Setup project with CLI | 7 | 10 | 10 |
| Development | 10 | 5 | 10 |
| Test | 8 | 10 | 10 |
| Build | 6 | 9 | 7 |
| Deploy | 3 | 10 | 10 |
| Debug | 10 | 10 | 10 |
| Scale | 10 | 10 | 10 |
| Performance | 2 | 8 | 10 |
| Package size | 4 | 2 | 5 |
| Maintain | 10 | 10 | 10 |
| Sum |   | 693 | 693 |

In the following, some of the ratings from the decision matrix are taken apart, and some additional drawbacks, as well as benefits of both technologies are assessed

<a name="frontendlearn"></a>
### 4.1.1 Learn 

Few months after the release of React, Pete Hunt held a conference talk named &#39;React: Rethinking best practices&#39; where he talked about different well established best practices and how Facebook changed some of them with their design choices of React (Hunt, 2013, 0:50–29:30). One-way data binding and the functional approach to UI were quite different from what the community was used to (Occhino &amp; Jordan Walke, 2013, 0:00–4:45). Ember is dependent on jQuery &#9998;, thus using a popular library to bind events and interact with the DOM. Consequently, Ember and React + Redux have different learning curves. The ecosystem of React is significant enough to influence all criterion from the decision matrix; Therefore, excellent books, tutorials and official documentation have been establishing since React got open sourced. Nonetheless, the concepts that are introduced to React are disparate, especially for developers coming from an object-oriented background. In contrast, Ember uses the well-established MV\* pattern and shares similarities to a Ruby MVC framework called &#39;Ruby on Rails&#39; by using convention over configuration. (Cravens &amp; Brady, 2014, 8f) While Ember also has a learning curve, it is evidently easier to learn than React.

<a name="frontendcli"></a>
### 4.1.2 CLI 

&quot;JavaScript Fatigue&quot; is a term created by Eric Clemmons in a popular article, which described the JavaScript ecosystem and an overwhelming amount of technologies that must be mastered before setting up a project. (Clemmons, 2015) Nowadays, JavaScript must be transpiled &#9998; to older ECMAScript versions that work across all browsers. JSX (when using React) should also be converted to JavaScript while preprocessors &#9998;, code splitting &#9998;, code minification require extra tools to optimize the user experience and to enhance the development workflow. (Banks &amp; Porcello, 2017, p. 2)A command line interface allows one to create a project with ease and is meant to cure the JavaScript fatigue by abstracting all the configurations while only exposing few commands to the developer.

Ember had a good CLI, called Ember-CLI, from almost the dawn of the framework. Facebook added their CLI &#39;Create React App&#39; (Abramov et al., 2016) to their open source collection in July 2016. Both tools get rid of JavaScript Fatigue exceptionally well and are much easier to use than the conventional, manual techniques. (Occhino, 2017, 2:55–3:50)

<a name="frontenddevelopment"></a>
### 4.1.3 Development 

Regarding development capabilities, React is undeniably the better choice. More libraries and tools have been entrenching to its ecosystem in comparison to Ember. (Att. 2 – React and Ember ecosystem) Following table showcases community differences by listing GitHub data (Data from 10.07.2017) of both technologies.

**3. Table – 
<a name="thirdtable"></a>Front end: GitHub comparison** 

| Framework | Issues | Stars | Issue/Star Ratio | Pull Requests |
| --- | --- | --- | --- | --- |
| React (Clark et al., 2013) | 620 | 70.593 | 0,008783 | 134 |
| Ember (Katz et al., 2011) | 248 | 18.034 | 0,013752 | 105 |

The number of pull requests and number of contributors (Data from 15.08.2017) – 1.044 React; 679 Ember – show that both communities are active. Consequently, the &#39;issue/star ratio&#39; of both technologies were lower than those of some other frameworks. (For instance, Angular had 1.564 issues and 25.676 stars, thus a ratio of 0,060913 [Data from 15.08.2017])

Furthermore, JSX allows developers to write JavaScript and HTML combined, thus is an intuitive technology for web developers. On the other hand, Ember uses Handlebars that tries to mimic JavaScript but has a different syntax and is meant to be a logic less template engine. Michael Jackson who worked on Mustache.js, which is a subset and mostly compatible to Handlebars, described the development of the template engine as &quot;reinventing a programming language&quot; (Jackson &amp; Florence, 2016, 9:52–10:20) and was glad to see the breakthrough of JSX.

<a name="frontendtestbuilddeploy"></a>
### 4.1.4 Test, Build, Deploy 

Both technologies have excellent tools to build, test and deploy products with. Ember solely uses the Ember CLI, while React refers to its own CLI or alternatively, manual usage of tools such as Gulp and Webpack &#9998;. When a project grows to the size where the custom configuration is mandatory, it is possible to eject the project from Create React App. Afterwards, developers need to learn how to use the tools given the fact, that a project ejection cannot be reverted. With Ember, it is possible to manually configure files, while still benefiting from the Ember CLI. The project does not have to be ejected and arising issues can mostly be solved through the installation of a suited add-on.

Ember has the unit testing framework QUnit (Zaefferer et al., 2008) and test runner Test&#39;em (Ho et al., 2011) integrated, but allows third party libraries likewise. The flexibility and minimalistic approach of React is also noticeable when it comes to automated tests. Incidentally, Facebook uses and recommends using Jest, (Nakazawa et al., 2014) which is also included in their CLI, to test web applications; However, React does not incorporate an integrated testing library. (Nakagawa, 2017)

<a name="frontendscaleperformancemaintain"></a>
### 4.1.5 Scale, Performance, Maintain 

Amadeus GUI does not require a lot of complex rendering. As a result, performance is almost a negligible criterion on its own; However, what Amadeus is concerned about is how well the framework scales with an ever-growing application, as well as how well the framework is maintained. Consequently, scalability and maintainability are one of the most important aspects of choosing a framework for Amadeus. Ember and React + Redux scale exceptionally well. Ember helps developers to maintain a good folder structure and forces developers to embrace the MV\* pattern. At the same time, React was developed with the intention to create a predictable, scalable and declarative JavaScript framework. (Occhino et al., 2014, 8:25–10:00) Facebook alone uses about 30.000 React components. (Abramov, 2017)

The expected longevity of the frameworks can be seen when looking at releases, major companies adopting the frameworks and size of the community. While the Ember community is seemingly smaller, it is a framework that has been around for more than 5 years, which is &quot;measured in web framework years, [...] an eternity.&quot; (Katz, 2017, 01:05–01:15) Above all, major companies like Twitch and LinkedIn employ some contributors of Ember and use it (Dale, 2017b; Suzuki, 2013), while React is maintained by Facebook and a huge open source community.

Regarding performance, the new Glimmer and the fiber implementation are both doubtlessly fast enough for Amadeus. Nevertheless, React has significant performance advantages in comparison to Ember. Running a framework benchmark test (Krause et al., 2015) shows significant differences between the two technologies. The values are in milliseconds. The test ran on a 64bit Windows (Version 1703, Build 15063.483) virtual machine with an Intel i7-2600 CPU (3.40GHz, 3GB RAM) and Chrome v.60.0.3112.90. The results are in milliseconds.

<a name="firstfigure"></a>
![Statistic of 10.000 row creation. It takes Ember 8519.045 ms and React 4771.61 ms ](./pictures/Create10000rows.png?raw=true "Inserting 10.000 rows")

**1. Figure – Performance: create 10.000 rows** 

The first figure shows the performance perks of the Fiber implementation when creating new DOM elements. React is almost 1.8 times faster than its counterpart. Other benchmark tests demonstrate that the new Glimmer virtual machine can almost keep up with the virtual DOM of React. The following figure shows the time spent to update rows.

<a name="secondfigure"></a>
![Statistic of updating every 10th row. It takes Ember 1936.595 ms and React 953.955 ms ](./pictures/UpdateEvery10throw.png?raw=true "Updating every 10th row")

**2. Figure – Performance: update every 10th row** 

<a name="frontendpackagesize"></a>
### 4.1.6 Package size 

Both technologies come at a relatively expensive cost. The package size of both technologies is big enough to decrease the user experience on mobile devices with slow internet access. Especially when building progressive web apps, package size and primal loading times are important. Fortunately, internet bandwidth keeps getting better (Roberts, 2000, 117f) and recent versions of React and Ember convincingly decreased their respective package size. (Beale, Thoburn, &amp; Navasardyan, 2017)

Printing a &lt;p&gt; Hello World &lt;/p&gt; produces a minified and gzipped file size of 197.73kb for Ember and 47.49kb for React. Redux is almost negligible due to its small size. Adding Redux increases the file size to 48.35kb. Subsequently, React has a much smaller, optimized file size.

<a name="frontenddecision"></a>
### 4.1.7 Decision 

To summarize the front-end comparison between React and Ember, it should be clear that both frameworks have their advantage and disadvantages. React has a bigger community while Ember allows developers to be productive faster. Additionally, the add-on structure of the Ember CLI allows more customization in comparison to the relatively new Create React App. Nonetheless, React did not only achieve to rethink best practices in their user base, but also across the entire community; Therefore, more frameworks seem to adopt some of the functional paradigms of React.

Due to the fact, that both frameworks scored 693 points for the use-case – Amadeus, the decision had to be based on less decisive factors. Seeing that Datex already has a lot of code written in Ember and the attractiveness of convention over configuration, let to the decision to use Ember for the futuristic Amadeus. Another reason was the mentality of Ember summarized by Tom Dale, a contributor to Ember, as being &quot;shameless to steal great ideas&quot; from other technologies in the market. &quot;In my mind, the strength of Ember and the reason why it has its longevity is because we don&#39;t have a problem saying: &#39;[...] the way we were doing it before was bad. Let&#39;s do it this new way and make sure that [...] there is a path of transitioning.&#39;&quot; (Dale &amp; Yehuda, 2014, 50:10–50:45)

<a name="backend"></a>
## 4.2 Back end 

Initially, developers of Datex listed well-known back-end languages. Afterwards, each item of the list was assessed based on user stories of the current Amadeus, removing many languages in the process. As the scope of viable technologies got smaller, the requirements had to be strictly adjusted to find viable differences between the technologies, that ultimately lead to a decision. The original list contained languages such as Java, PHP, C#, Python, Ruby, Node.js, Erlang &#9998; , Scala and Go &#9998; . Due to some obsolete architectures from older languages, size of community constraints and missing developer experience with certain languages, the closer selection contained only Scala and Node.js as viable possibilities for the rework of the Amadeus backend.

Following table shows all criteria with their respective description.

<a name="forthtable"></a>
**4. Table – Back end: Selection criteria with description**

| Selection criteria | Description |
| --- | --- |
| Learn | Effort to learn the technology. |
| Development | Community, ecosystem, IDE support. |
| Test | Testing tools. |
| Secure | Prevention of SQL injection and other potential vulnerabilities. |
| Build | Build tools. |
| Deploy | Effort to push applications to production and deploy them. |
| Scale | Scalability of the application and performance with a growing code base. |
| Maintain | Backwards compatibility, longevity. |

<a name="backendlearn"></a>
### 4.2.1 Learn 

Since Node.js is simply JavaScript in conjunction with C++ and C modules, it is easy to learn. The concept of non-blocking I/O inside a single-threaded language, can be intimidating to beginners. On the other hand, especially coming from a multi-threaded, blocking I/O language, developers tend to quickly grasp the power of the architecture that is unleashed when using the event-loop to its full potential. Contrary to the learning curve of Node.js is the learning curve of Scala. It takes a while not only to comprehend the complex syntax of Scala but also to understand the functional programming paradigm. The documentation and other learning resources are excellent for both technologies, but considering that JavaScript must be learned anyhow to develop a front end, Node.js distinctly has an advantage and saves teams a lot of resources.

<a name="backenddevelopment"></a>
### 4.2.2 Development 

While Scala is maintained with a high academic standard and allows access to all JVM related technologies such as an enormous collection of maven repositories, the community and ecosystem is nowhere near the ecosystem of Node.js.

<a name="fifthtable"></a>
**5. Table – Back end: GitHub comparison** (Data from 17.07.2017

| Language | Issues | Stars | Issue/Star Ratio | Pull Requests |
| --- | --- | --- | --- | --- |
| Scala | 2.042 | 8.521 | 0,239643 | 66 |
| Node.js | 647 | 37.064 | 0,017456 | 320 |

The fifth table showcases the differences between the two technologies. Not only the bare size of the community but also the number of JavaScript packages have skyrocketed and quickly surpassed the Maven repository, which has been around for more than 20 years. As per a web application that counts the number of modules, there are 503.307 npm JavaScript repositories with an average growth of 482 modules per day while Java seems to plateau on close to 200.000 maven repositories with an average growth of 90 modules per day. (Debill, 21.08.2017)

<a name="backendtestsecurebuilddeploy"></a>
### 4.2.3 Test, Secure, Build, Deploy 

Scala and Node.js can make use of several libraries to test applications. Scala has an additional advantage due to the nature of pure functions. Both technologies can make use of test-driven development, thus providing excellent code quality management tools.

In terms of security, Scala has the advantage of the proven JVM architecture while still being exposed to some vulnerabilities at times (Play, 2017). Node.js and related popular frameworks such as Express occasionally find vulnerabilities that haven&#39;t been found before. (Dawson, 2017; Node.js, 2017)

The deployment process is good and similar on both sides. It is mainly dependent on the hosting service and both technologies are independent of the underlying operating system of the server.

Furthermore, the JavaScript ecosystem supports a lot of different tools to minify, transpile and transform JavaScript. None of the tools are required when working with Node.js because there are no concerns that the code runs on some old browser, which means that always the newest ESNext ECMAScript standard can be used. Scala must be compiled to Java bytecode and is then ready to be deployed.

<a name="backendmaintain"></a>
### 4.2.4 Maintain 

ECMAScript makes mainly backward compatible changes and many of the ESNext features that are in a lower TC39 stage can be used through additional libraries. With a growing number of external repositories, it is easy to lose track of breaking changes that are being applied to the packages in use. Most of the times it is still more convenient to use a preexisting package and read through the API instead of reinventing the wheel. Scala has similar problems and in addition, is not entirely binary compatible between different releases. (Odersky, 2011; Miller, 2017)

The Stack Overflow survey from 2017 placed JavaScript as the most commonly used programming language while Java took the third place. Both, Scala and JavaScript are with roughly 60% loved amongst their community. Additionally, Node.js is with 62.1% the second most wanted technology. (Stack Overflow, 2017) All the above indicate active communities and increases the expected longevity of both languages.

<a name="backendscale"></a>
### 4.2.5 Scale 

Scala scales extremely well. It is a static typed language and the functional paradigm allows to write short, precise code. Frameworks and libraries also help with the usage of concurrency and it is dynamic in the sense that either blocking or non-blocking I/O is possible.

In JavaScript, developers had to deal with nested callback functions for years. The introduction of &#39;promises&#39; and the &#39;async/await&#39; keywords helped the application scalability in terms of code readability. (Rauschmayer, 2017a) Nevertheless, the dynamically typed nature of JavaScript makes a scaling code-base difficult. The problem can be solved by making use of additional technologies. Microsoft introduced TypeScript in October 2012. It is a strictly typed superset of JavaScript and is meant to fix some of the issues of JavaScript. (Hejlsberg et al., 2012) According to the biggest developer survey in 2017, TypeScript scored an additional 4.3% on the question about the most loved language, leveraging it to the third place in comparison to the 11th place of JavaScript. (Stack Overflow, 2017)

Due to the non-blocking structure, Node.js was faster in all the performance tests conducted by the author. (Att. 3 – Back-end performance) Generally speaking, Node.js should be used when an application is heavily I/O dependent and Scala if a lot of computing is required. (Brikman, 2014)

<a name="backenddecision"></a>
### 4.2.6 Decision 

<a name="sixthtable"></a>
**6. Table – Back end: Decision matrix**

| Selection criteria | Weight | Node.js + TypeScript | Scala |
| --- | --- | --- | --- |
| Learn | 10 | 8 | 5 |
| Development | 10 | 10 | 7 |
| Test | 8 | 10 | 10 |
| Secure | 10 | 8 | 9 |
| Build | 2 | 10 | 9 |
| Deploy | 2 | 10 | 10 |
| Maintain | 10 | 9 | 9 |
| Scale | 10 | 9 | 9 |
| Sum |   | 560 | 508 |

The sixth table shows the weight of each criteria and the rating based on all the above analysis. Regarding Amadeus, the result show clear advantages of Node.js in comparison to Scala. On the one hand choosing TypeScript added another technology to the learning process and forces developers to be more restricted in the way they code. On the other hand, IntelliSense with TypeScript works better; thus, enhancing the development workflow. Furthermore, applications scale better with a strictly typed language, ultimately resulting in a less error prone code base; Therefore, using TypeScript improved the rating of several criteria. Despite the fact, that we already have more than 9.000 lines of Scala code across 112 files, we still think choosing Node.js is a better long-term investment. Picking Node.js in a project is less resource intensive and allows code sharing between the front – and back end since the whole development stack will be written or compiled to JavaScript. Additional technologies and tools such as IDE configurations, Linter, code prettier and testing libraries must be learned only once across the development stack.

<a name="migrationpath"></a>
# 5. Migration path 

To follow up on the fact, that customers have been using a desktop application for several decades, we decided to make use of Electron.js. Electron allows to &quot;quickly write sophisticated cross-platform desktop apps.&quot; (Jensen, 2017, p. xvii) Since Node.js is used by Electron anyhow, we remove additional language barriers by developing a web application and a desktop application from mostly the same code-base. (Jensen, 2017, 4f) Electron supports building desktop apps with Ember (Rieseberg, 2016, 0:30–15:00) and fully supports TypeScript. (Sikelianos, 2017) Additionally, since Ember has full TypeScript support as well, we can take full advantage of the JavaScript superset by using it in conjunction with Ember for the front-end alike. Thus, the whole code-base will be consistent and written in TypeScript. Ken Pugh described consistency as a &quot;form of simplicity&quot; while advocating that enforcing consistency should always follow a purpose. (Pugh, 2005, p. 31) In our use-case, consistency enables Datex to establish full-stack guidelines, code reviews, and testing design patterns to enhance quality management and productivity.

To overcome some anticipated migration problems, developers started working on a centralized server called Starserver a year ago. The Starserver is entirely written in C# and is meant to solve some VB6 issues by allowing mutual communication from and to Amadeus. The interface works through a TCP/Remote Method Invocation (RMI) &#9998; library (Kalkan &amp; Cleaver, 2013) and a COM wrapper. At the time of writing, the development of the Starserver is finished and developers are starting to not only migrate C# DLLs, but also to add new features, to the Starserver.

<a name="thirdfigure"></a>

![Amadeus is connected to 40 'raw' DLL's which will be migrated to the Starserver. At the same time, web development of the futuristic Amadeus starts.](./pictures/AmadeusNow.png?raw=true "Rewrite of Amadeus and Starserver migration")

**3. Figure – Migration phase #1: Rewrite of Amadeus &amp; Starserver migration** 

At the same time, as seen in the third figure, developers can start the reimplementation of Amadeus with the proposed technologies from this paper. The already written Craftmanportal must be migrated from Scala to Node.js and every Amadeus user story that is implemented in the legacy code base, must be resembled in the futuristic Amadeus. Furthermore, the Starserver is connected to the database whereas single C# DLLs had no database access and were fully reliant on information passed by the VB6 code through COM interoperability. Every service that gets migrated to the Starserver can access the database. As a result, less COM dependent communication is required, removing code complexity and DLL hell in the process.

<a name="forthfigure"></a>
![The legacy code base is connected to a single instance of the Starserver via Socket, RMI and COM. Both the legacy code and the Starserver have access to the database.](./pictures/AmadeusLater.png?raw=true "Rewrite of Amadeus and adding features")

**4. Figure – Migration phase #2: Rewrite of Amadeus &amp; adding features** 

Figure 4 depicts the infrastructure once the Starserver migration is finished. Only one DLL will be required, ultimately getting rid of a lot of code verbosity. During this migration phase, all the developers can solely focus on adding more features to Amadeus (Starserver) and the futuristic – progressive web application – Amadeus.

<a name="fifthfigure"></a>
![We have one web application (Ember) and a desktop application (Ember + Electron). Either the clients are connected to both, Starserver and Node.js server, or to only Node.js.](./pictures/AmadeusWeb.png?raw=true "Progressive, ambitious web application")

**5. Figure – Migration phase #3: Progressive, ambitious web application**

At the time, the web application is going to contain the same functionality as the VB6 legacy code, we can get rid of VB6 entirely and additionally make use of all the features that were implemented into the Starserver during the entire migration process. There are different ways to make use of the code inside of the Starserver.

One option is to transform the Starserver into a Representational State Transfer (REST) &#9998; server. This would result in clients connecting to both Node.js and the Starserver via HTTP. Alternatively, due to the flexible nature of Node.js, servers can act as clients and communicate mutually with other servers or services (Springer, 2013, p. 24); Thus, there are more possibilities to connect to the Starserver. The Node.js server could use a similar approach to the VB6 server as seen earlier in the fourth figure and make use of sockets. It could also send HTTP requests in case we use a RESTful Starserver architecture, or as depicted in the fifth figure, use the code of the Starserver directly through a library called Edge.js. (Janczuk et al., 2013) Edge.js is a library that allows the usage of .NET code, conclusively lowering the latency between cross-server requests by a lot. (Att. 4 – Latency comparison) A decision has yet to be concluded because, at the time we reach the end of the second migration phase, there might be other viable alternatives.

<a name="conclusion"></a>
# 6 Conclusion 

Modern web development has enormous potential, and all the listed technologies would not be available without an active open source community. While some people believe that the growing complexity of different technologies and what seems to be a myriad of new tools emerging into the market daily are a contradiction to technological advancement, constant improvements of web technologies make solutions feasible that could not be thought of before. Dijkstra reasoned the flawed thought that advancing programming technologies would make programming easier in 1972:

&quot;[…] I would like to insert a warning to those who identify the difficulty of the programming task with the struggle against the inadequacies of our current tools, because they might conclude that, once our tools will be much more adequate, programming will no longer be a problem. Programming will remain very difficult, because once we have freed ourselves from the circumstantial cumbersomeness, we will find ourselves free to tackle the problems that are now well beyond our programming capacity.&quot; (Dijkstra, 1972, 860f) In other words, present-day development obligates developers to learn additional technologies but also provides new problem-solving methods; Therefore, what is often described as fatigue is, in fact, the possibility to solve a problem, frankly at the cost of additional effort, which was not solvable before.

Regarding the migration, an alternative approach was to reimplement the entire Amadeus application in C# first, then afterwards migrate to modern web technologies. However, the beauty of the migration process, proposed in the scientific work is that we do not need to touch the obsolete VB6 code base to advance Amadeus because additional features can be added to the Starserver directly. The added functionality can be used by the futuristic Amadeus alike; Subsequently, the migration path allows for the least amount of overhead while still improving the current version of Amadeus.

The technologies proposed in this paper enable a reimplementation of Amadeus from an obsolete Visual Basic application to a sophisticated, ambitious, progressive web application while increasing code quality and developer productivity in the process. Furthermore, there are huge economic benefits of writing a cross-desktop application as well as providing users an intuitive web UI through a progressive web application. Moreover, the choice to make use of Node.js, Electron, and Ember in conjunction with TypeScript does not only enable a scalable development stack but also qualifies front end developers to become full stack developers easily. At the same time, back end developers have an easier time transitioning into a full stack role alike.

The longevity of the technologies is hard to anticipate and while dying technologies will always be expensive, with the proposed technologies we will have the possibility of maintaining and adjusting the code ourselves. Additionally, the sheer size of the respective communities and ecosystem should allow transitioning to innovative technologies with ease. A foresight of web development in several years is impossible to predict, but I personally believe that with emerging technologies such as WebAssembly which is a low level, browser-, language- and hardware independent compile target (Haas et al., 1ff), the web will be more relevant than ever before. JavaScript will either be compiled into or used in conjunction with code from languages compiled into WebAssembly, resulting in even more flexibility regarding web programming languages.

Time will tell how much the development productivity, quality and performance of Amadeus will improve. Nonetheless, emphasizing on the fact, that the community changes rapidly and that we might be on the verge of the next bleeding edge technology, which could quickly change and revolutionize what is now considered to be best practices; it has never been more exciting to be a web-software developer.

***
&#10071; Thank you for reading. We are currently hiring. If you are interested working with the proposed technologies, send us an email info@datex.de
***

<a name="glossary"></a>
# Glossary 

**Architecture reconstruction** &quot;is the process where the &#39;as-built&#39; architecture of an implemented system is obtained from the existing legacy system.&quot; (Kazman, O&#39;Brien, &amp; Verhoef, 2002, vii)

**Backwards compatibility** describes new specifications that don&#39;t break the functionality of existing applications when upgrading the respective technology in use.

**Bleeding edge technology** is a – regarding popularity, unreliable – technology that could either be relevant or irrelevant in a short amount of time.

**Code splitting** is the process of splitting code into different independent bundles to reduce the load time of a web application and use the code on demand. (Koppers et al., 2014)

**Component Object Model** enables interoperability to communicate between managed code (e.g. C#) and unmanaged code (e.g. VB6).

**Disruptive innovation** refers to new emerging technologies that disrupts the current market for the sake of innovation.

**Document Object Model** is a tree of HTML elements that represents the hierarchy of the elements.

**Dynamic Link Library** is a file format, can be consumed by applications and contains code or data.

**ECMAScript** defines standards for the JavaScript language.

**Electron.js** combines Chromium and Node.js to write desktop applications with web technologies (HTML, CSS, JS).

**Erlang** is a general-purpose programming language to build real-time systems. (Gustavsson et al., 1987)

**Event loops** allow asynchronous code execution in JavaScript.

**Explicit typed** languages are languages that require explicit type declarations.

**Go** or golang is an open source programming language by Google. (Cox et al., 2009)

**Gzip** is a file format to compress the file size and is included in the HTTP specification. (Fielding, Gettys, Mogul, Frystyk, &amp; Berners-Lee, 1999, p. 22)

**Java Virtual Machine** runs Java bytecode; Hence, executes Java programs.

**jQuery** is a JavaScript library to manipulate the DOM.

**JSX** combines HTML and JavaScript to produce React elements, which can be rendered to the DOM. (Lacker, 2016a)

**Minified** stands for the minification process of web technology files to reduce the file size and ultimately improve the loading experience for the user.

**Model View Controller** is an architecture to build graphical user interfaces and is mainly used in web applications.

**Preprocessor** describes the technology used to process viz. compile or transpile code into a different output format.

**Remote Method Invocation** is an implementation to communicate across different systems or languages. (Waldo, 1998, 12f)

**Representational State Transfer** is a web service that enables communication within distributed systems. (Fielding, 2000, pp. 76–105)

**Static typed languages** are languages that know the type of a variable at compile time. This can be done through either explicit type declarations or type interference.

**Transpiling** is the process of converting one language into another with similar abstraction levels. (Fenton, 2012)

**TC39** stands for technical committee 39 which specifies the ECMAScript standard. (Rauschmayer, 2017b)

**Visual Basic Classic** describes the latest Visual Basic version; Thus, Visual Basic 6.

**Visual Basic** is an object-oriented programming language from Microsoft.

**Webpack** bundles JavaScript code and supports different plugins to enhance web development and the user experience. (Koppers et al., 2012)

<a name="attachments"></a>
# Attachments 

<a name="firstattachment"></a>
**1. Attachment – Market share operating systems** 

| **Operating system** | **Market share** |
| --- | --- |
| Windows 7 | 49,10% |
| Windows 10 | 18,88% |
| Windows XP | 9,94% |
| Windows 8.1 | 8,63% |
| Mac OS X 10.11 | 3,74% |
| Windows 8 | 2,28% |
| Linux | 2,00% |
| Mac OS X 10.10 | 1,82% |
| Windows Vista | 1,29% |
| Mac OS X 10.9 | 0,71% |
| Mac OS X 10.12 | 0,50% |
| Mac OS X 10.7 | 0,26% |
| Mac OS X 10.6 | 0,25% |
| Mac OS X 10.8 | 0,25% |

(Netmarketshare, 2016)

<a name="secondattachment"></a>
**2. Attachment – React and Ember ecosystem** 

As of 15.08.2017, Ember has 5230 packages. (Node Package Manager, 2017a)

As of 15.08.2017, React has 35424 packages. (Node Package Manager, 2017b)

<a name="thirdattachment"></a>
**3. Attachment – Back-end performance** 

The benchmark tests were not written by the author, but the source code was analyzed and the results were verified. The numbers represent JSON responses per second. Play and Akka are both Scala frameworks, whereas only the fastest of the two is represented in the tables.

JSON serialization

|  |  |
| --- | --- |
| Play2-scala | 240,171 |
| Node.js | 372,531 |

Single database query

|  |  |
| --- | --- |
| Play-scala-anorm | 15,888 |
| Node.js | 143,245 |

Multiple database queries

|  |  |
| --- | --- |
| Akka-http | 7,180 |
| Node.js | 7,210 |

Fortunes

|  |  |
| --- | --- |
| Akka-http | 6,823 |
| Node.js | 101,276 |

Data updates

|  |  |
| --- | --- |
| Akka-http | 2,038 |
| Node.js | 2,196 |

Plaintext

|  |  |
| --- | --- |
| Play2-scala | 421,080 |
| Node.js | 429,494 |

(Smith, Turner, &amp; Malawski, 2017)

<a name="forthattachment"></a>
**4. Attachment – Latency comparison** 

![Latency comparison. In-process call from Node.js to C# via Edge.js takes 0.0464 ms while cross-process, via HTTP takes 1.4813 ms](https://camo.githubusercontent.com/15bfeb4bb415a2889acc3d58f1c3be7e70fea486/68747470733a2f2f662e636c6f75642e6769746875622e636f6d2f6173736574732f3832323336392f3438363339332f36343566363936612d623932302d313165322d386132302d3966613639333262623039322e706e67)

(Janczuk, 2013)

# References

Abramov, D. (2015a). React Components, Elements, and Instances: Top-Down Reconciliation. Retrieved from <https://facebook.github.io/react/blog/2015/12/18/react-components-elements-and-instances.html#top-down-reconciliation>

Abramov, D. (2015b). Why use Redux over Facebook Flux? Author of Redux in an Q&amp;A answer. Retrieved from <https://stackoverflow.com/questions/32461229/why-use-redux-over-facebook-flux>

Abramov, D. (2017). When will react-fiber be officially released: React maintainer answers GitHub issue. Retrieved from <https://github.com/facebook/react/issues/9463#issuecomment-295643228>

Abramov, D., Dorr, T., Bannard, L., Erikson, M., Molinari, N., Clark, A.,. . . Carpenter, K. (2015). Redux. GitHub. Retrieved from <https://github.com/reactjs/redux>

Abramov, D., Haddad, J., Immonen, V., Chedeau, C., Stoiber, M., Fadlil, A. V.,. . . Sorokobatko, V. (2016). Create React App. GitHub. Retrieved from <https://github.com/facebookincubator/create-react-app>

Banks, A., &amp; Porcello, E. (2017). _Learning React: Functional web development with React and Redux_ (First edition). Sebastopol, CA: O&#39;Reilly Media.

Beale, M., Thoburn, C., &amp; Navasardyan, A. (2017). Ember 2.14 and 2.15 Beta Released. Retrieved from <https://emberjs.com/blog/2017/07/06/ember-2-14-released.html>

Brikman, Y. (J.). (2014). _Node.js vs Play Framework_ [Video]. Tokyo: ScalaMatsuri. Retrieved from <https://www.youtube.com/watch?v=b6yLwvNSDck&amp;feature=youtu.be&amp;t=37m50s>

Burgess, M. (2017). _Ember for Artisans: Creating Single Page Apps backed by Laravel_. Leanpub: Leanpub.com

Chiusano, P., &amp; Bjarnason, R. (2015). _Functional programming in Scala_. Shelter Island: Manning

Clark, A., Hunt, P., Lou, C., Alpert, S., Markbåge, S., Chedeau, Shannessy, Paul O&#39;,. . . Vaughn, B. (2013). React. GitHub: Facebook. Retrieved from <https://github.com/facebook/react>

Clark, L. (2017). _A Cartoon Intro to Fiber_ [Video]. California: React Conf. Retrieved from <https://www.youtube.com/watch?v=ZCuYPiUIONs>

Clemmons, E. (2015). JavaScript Fatigue. Retrieved from <https://medium.com/@ericclemmons/javascript-fatigue-48d4011b6fc4>

Collins, B. E., &amp; Guetzkow, H. (op. 1964). _A social psychology of group processes for decision-making_. New York: Wiley.

Cox, R., Pike, R., Griesemer, R., Fitzpatrick, B., Taylor, I. L., Gerrand, A.,. . . Hara, M. (2009). Go. GitHub: Google. Retrieved from <https://github.com/golang/go>

Cravens, J., &amp; Brady, T. Q. (2014). _Building Web applications with Ember.js_. Beijing: O&#39;REILLY.

Crockford, D. (2009). _JavaScript: The Good Parts_ [Video]. Malmö, Sweden: Øredev. Retrieved from <http://oredev.org/oredev2009/videos/javascript--the-good-parts.html>

Dahl, R. (2009). _Node.js: Evented I/O for V8 Javascript_ [Video]: JSConf. Retrieved from <https://www.youtube.com/watch?v=ztspvPYybIY>

Dale, T. (2017a). Change Tracking with Tracked Properties: The Immutable Pattern. Retrieved from <https://glimmerjs.com/guides/tracked-properties>

Dale, T. (2017b). _Tom Dale Talks Ember_ [Video]: LinkedIn. Retrieved from <https://engineering.linkedin.com/blog/2017/04/om-dale-talks-emberjs>

Dale, T., &amp; Yehuda, K. (2014). _The Road to Ember 2.0_ [Audio]: Changelog. Retrieved from <https://changelog.com/podcast/131>

Dawson, M. (2017). Security updates for all active release lines. Retrieved from <https://nodejs.org/en/blog/vulnerability/july-2017-security-releases/>

Debill, E. Module Counts [Web application]. Retrieved from <http://www.modulecounts.com/>

Decker, K., Katz, Y., Johnson, A., &amp; Knappmeier, N. (2010). Handlebars.js. GitHub. Retrieved from <https://github.com/wycats/handlebars.js>

Dijkstra, E. W. (1972). The humble programmer. In M. Vardi (Ed.), _Communications of the ACM_ (pp. 859–866). New York, N.Y.: Association for Computing Machinery.

Dodds, K. C., Abramov, D., &amp; Clark, A. (2016). _Why, What, and How of React Fiber with Dan Abramov and Andrew Clark_ [Video]. Retrieved from <https://www.youtube.com/watch?v=crM1iRVGpGQ&amp;feature=youtu.be&amp;t=2m40s>

Fenton, S. (2012). Compiling vs Transpiling. Retrieved from <https://www.stevefenton.co.uk/2012/11/compiling-vs-transpiling/>

Fielding, R., Gettys, J., Mogul, J., Frystyk, H., &amp; Berners-Lee, T. (1999). _Hypertext transfer protocol--HTTP/1.1_. RFC 2616: Network Working Group.

Fielding, R. T. (2000). _Architectural Styles and the Design of Network-based Software Architectures_ (Dissertation). University of California, Irvine, California.

Galli, M., &amp; Perrier, J.-Y. (2003). Inner-browsing extending the browser navigation paradigm. Retrieved from <https://developer.mozilla.org/en-US/docs/Archive/Inner-browsing\_extending\_the\_browser\_navigation\_paradigm>

Gustavsson, B., Dahlberg, B.-E., Eriksson, S., Andin, I., Larsson, L., Green, R.,. . . Gudmundsson, D. (1987). Erlang. GitHub. Retrieved from <https://github.com/erlang/otp>

Haas, A., Rossberg, A., Schuff, D. L., Titzer, B. L., Holman, M., Gohman, D.,. . . Bastien, J. F. Bringing the web up to speed with WebAssembly. In A. Cohen &amp; M. Vechev (Eds.), _the 38th ACM SIGPLAN Conference_ (pp. 185–200). <https://doi.org/10.1145/3062341.3062363>

Hejlsberg, A., Rosenwasser, D., Hegazy, M., Matveev, V., Sanders, Shively-Sanders, Nathan, Nandi, S.,. . . Freeman, J. (2012). TypeScript. GitHub: Microsoft. Retrieved from <https://github.com/Microsoft/TypeScript>

Ho, T., Würbach, J., Verbaten, J., Lima, I. R., Zamir, B., Karns, J.,. . . Penner, S. (2011). Test&#39;em Scripts! GitHub. Retrieved from <https://github.com/testem/testem>

Hunt, P. (2013). _React: Rethinking best practices_ [Video]. Berlin: JSConf EU. Retrieved from <https://www.youtube.com/watch?v=fg3DAkYjCW8>

Jackson, M., &amp; Florence, R. (2016). _React Router v4_: Netflix. Retrieved from <https://www.youtube.com/watch?v=Vur2dAFZ4GE&amp;feature=youtu.be&amp;t=9m52s>

Janczuk, T. (2013). Performance: Edge.js is 32x faster than a cross-process call. Retrieved from <https://github.com/tjanczuk/edge/wiki/Performance>

Janczuk, T., Stratman, L., Mavity, B., Beletsky, A., Bäumer, D., Thorpe, D.,. . . Channon, J. (2013). Edge. GitHub. Retrieved from <https://github.com/tjanczuk/edge>

Jensen, P. B. (2017). _Cross-platform desktop applications: Using Electron and NW.js_. Shelter Island NY: Manning Publcations Co.

Kalkan, H. İ., &amp; Cleaver, O. (2013). SCS. GitHub. Retrieved from <https://github.com/hikalkan/scs>

Katz, Y. (2013). _Building Ambitious Web Apps with Ember.js_ [Video]. Philadelphia: Emerging Technology for the Enterprise Conference. Retrieved from <https://www.youtube.com/watch?v=fg3DAkYjCW8>

Katz, Y. (2017). _Ember and the State of Web Frameworks_ [Video]. Philadelphia: Emerging Technology for the Enterprise Conference. Retrieved from <https://www.infoq.com/presentations/ember-state-web-frameworks?utm\_source=presentations\_about\_javascript&amp;utm\_medium=link&amp;utm\_campaign=javascript>

Katz, Y., Chan, G., Jackson, R., Hietala, C., Dale, T., Muñoz, M.,. . . Beale, M. (2013). Glimmer-vm. GitHub. Retrieved from <https://github.com/glimmerjs/glimmer-vm>

Katz, Y., Dale, T., Selden, K., Penner, S., Silber, L., Jackson, R.,. . . Gengler, K. (2011). Ember.js. GitHub: Ember.js. Retrieved from <https://github.com/emberjs/ember.js/>

Kazman, R., O&#39;Brien, L., &amp; Verhoef, C. (2002). _Architecture Reconstruction Guidelines, 2nd Edition_. Fort Belvoir, VA: Defense Technical Information Center.

Koppers, T., Larkin, S., Jalan, S., Kumar, S., Mendes, W., Franco, D.,. . . Brown, A. (2012). Webpack. GitHub: Webpack. Retrieved from <https://github.com/webpack/webpack>

Koppers, T., Weindel, F., Sawardekar, D., Young, K. R., Schaefer, E., Phan, H.,. . . Dodds, K. C. (2014). Code Splitting. Retrieved from <https://webpack.github.io/docs/code-splitting.html>

Krause, S., Tarimo, S., Sorokin, L., Baptiste, Bo, Y., Yu, T.,. . . Oppitz, M. (2015). JS Framework Benchmark. GitHub. Retrieved from <https://github.com/krausest/js-framework-benchmark>

Lacker, K. (2016a). Introducing JSX. Retrieved from <https://facebook.github.io/react/docs/introducing-jsx.html>

Lacker, K. (2016b). Reconciliation. Retrieved from <https://facebook.github.io/react/docs/reconciliation.html>

Lehnardt, J., Jackson, M., Silva, D. d., Cherry, B., &amp; Johnsen, P. (2009). Mustache.js. GitHub. Retrieved from <https://github.com/janl/mustache.js/>

Maurer, H., &amp; Kulathuramaiyer, N. (2007). Coping With the Copy-Paste-Syndrome. In T. Bastiaens &amp; S. Carliner (Eds.), _E-learn 2007. World conference on e-learning in corporate, government, healthcare, &amp; higher education /  edited by Theo Bastiaens, Saul Carliner_ (pp. 1071–1079). Retrieved from <https://www.learntechlib.org/p/26479/>

McCune, R. R. (2011). Node.js Paradigms and Benchmarks, _STRIEGEL, GRAD OS F&#39;11_. Retrieved from <http://netscale.cse.nd.edu/cms/pub/Edu/GradOSF11FinalProjects/final.pdf>

Meijer, E. (2009). _Functional Programming Fundamentals: Chapter 1 of 13_ [Video]: Channel9. Retrieved from <https://channel9.msdn.com/Series/C9-Lectures-Erik-Meijer-Functional-Programming-Fundamentals/Lecture-Series-Erik-Meijer-Functional-Programming-Fundamentals-Chapter-1>

Michaelson, G. (2011). _An introduction to functional programming through Lambda calculus_ (Dover ed.). _Dover books on mathematics_. Mineola N.Y.: Dover Publications.

Miller, H. (2017). Binary compatibility of Scala releases. Retrieved from <http://docs.scala-lang.org/overviews/core/binary-compatibility-of-scala-releases.html>

Nakagawa, E. (2017). Testing React Apps. Retrieved from <https://facebook.github.io/jest/docs/en/tutorial-react.html>

Nakazawa, C., Abramov, A., Pierzchała, M., Pedrotti, M., Bekkhus, S., Carlesso, C.,. . . Nakagawa, E. (2014). Jest. GitHub: Facebook. Retrieved from <https://github.com/facebook/jest>

Netmarketshare. (2016). Desktop Operating System Market Share. Retrieved from <https://www.netmarketshare.com/operating-system-market-share.aspx?qprid=10&amp;qpcustomd=0&amp;qpcustomb=&amp;qpsp=2016&amp;qpnp=1&amp;qptimeframe=Y>

Node Package Manager. (2017a). Ember packages. Retrieved from <https://www.npmjs.com/search?q=ember&amp;page=1&amp;ranking=optimal>

Node Package Manager. (2017b). React packages. Retrieved from <https://www.npmjs.com/search?q=react&amp;page=2&amp;ranking=optimal>

Node.js. (2017). Security updates. Retrieved from <https://expressjs.com/en/advanced/security-updates.html>

Occhino, T. (2017). _React Fiber, Create React App and React Community: Keynote Part 4_ [Video]. California: React Conf. Retrieved from <https://www.youtube.com/watch?v=5Wd5rxT7e1U&amp;feature=youtu.be&amp;t=2m55s>

Occhino, T., Hunt, P., &amp; Chen, J. (2014). _Rethinking Web App Development at Facebook_ [Video]. San Francisco: F8 Developer Conference. Retrieved from <https://code.facebook.com/posts/1430798673841282/f8-developer-conference-hacker-way-recap/>

Occhino, T., &amp; Jordan Walke. (2013). _JS Apps at Facebook_ [Video]. Amelia Island: JSConf US. Retrieved from <https://www.youtube.com/watch?v=fg3DAkYjCW8>

Odersky, M. (2011). Binary compatibility: status and outlook. Retrieved from <http://www.scala-lang.org/old/node/9346>

Odersky, M. (2014). The Scala Language Specification: Version 2.9. Retrieved from <http://www.scala-lang.org/docu/files/ScalaReference.pdf>

Odersky, M., Spoon, L., &amp; Venners, B. (2010). _Programming in Scala_ (2nd ed.). Walnut Creek Calif.: Artima.

Penner, S., Jackson, R., Bieniek, T., Selden, K., Hammond, N., Bixby, J.,. . . Builes, A. (2013). Ember-CLI. GitHub. Retrieved from <https://ember-cli.com/>

Play. (2017). Security Vulnerabilities. Retrieved from <https://www.playframework.com/security/vulnerability>

Pratschner, S. (2001). Simplifying Deployment and Solving DLL Hell with the.NET Framework: Problem Statement. Retrieved from <https://msdn.microsoft.com/en-us//library/ms973843.aspx>

Pugh, K. (2005). _Prefactoring: Extreme abstraction : extreme separation : extreme readability /  Ken Pugh_. Beijing, Farnham: O&#39;REILLY.

Ram, S. Referential Transparency. Retrieved from <http://userpage.fu-berlin.de/~ram/pub/pub\_jf47ht81Ht/referential\_transparency>

Rauschmayer, A. (2017a). _Exploring ES2016 and ES2017: Async functions_. Leanpub: Leanpub.com. Retrieved from <http://exploringjs.com/es2016-es2017/ch\_async-functions.html>

Rauschmayer, A. (2017b). _Exploring ES2016 and ES2017: TC39 Process_. Leanpub: Leanpub.com. Retrieved from <http://exploringjs.com/es2016-es2017/ch\_tc39-process.html>

Rieseberg, F. (2016). _Building Desktop Apps with Ember and Electron_ [Video]. Portland: EmberConf. Retrieved from <https://www.youtube.com/watch?v=\_uA5LZk2vmQ>

Roberts, L. G. (2000). Beyond Moore&#39;s law: Internet growth trends. _Computer_, _33_(1), 117–119. <https://doi.org/10.1109/2.963131>

SABRY, A. M.R. (1998). What is a purely functional language? _Journal of Functional Programming_, _8_(1), 1–22. <https://doi.org/10.1017/S0956796897002943>

Scheffler, J. (2017). The History of Ember.js: An Interview With Tom Dale at EmberConf. Part One. Retrieved from <https://blog.heroku.com/history-of-emberjs>

Schlueter, I. Z. (2010). npm release. Retrieved from <https://github.com/npm/npm/releases?after=v0.1.1>

Shannessy, P. O., Davis, K., Fisher, B., Kim, E., Chedeau, C., Raspopov, A.,. . . Callister, J. (2014). Flux. GitHub: Facebook. Retrieved from <https://github.com/facebook/flux>

Sikelianos, Z. (2017). Announcing TypeScript support in Electron. Retrieved from <https://electron.atom.io/blog/2017/06/01/typescript>

Smith, M., Turner, H., &amp; Malawski, K. (2017). Web Framework Benchmarks: Round 14. Retrieved from <https://www.techempower.com/benchmarks/#section=data-r14&amp;hw=ph&amp;test=fortune>

Sndergaard, H., &amp; Sestoft, P. (1990). Referential transparency, definiteness and unfoldability. _Acta Informatica_, _27_(6). <https://doi.org/10.1007/BF00277387>

Springer, S. (2013). _Node.js: Das umfassende Handbuch_ (1st ed.). _Rheinwerk computing_. Bonn: Rheinwerk-Verl.

Stack Overflow. (2017). Developer Survey Results. Retrieved from <https://insights.stackoverflow.com/survey/2017>

Suzuki, J. (2013). Ember.js on the Twitch Directory. Retrieved from <https://blog.twitch.tv/ember-js-on-the-twitch-directory-46217fc465be>

Välimäki, M. (2005). _The rise of open source licensing: A challenge to the use of intellectual property in the software industry_. Dissertation (1st ed.). Helsinki Finland: Turre.

van Kesteren, A. (2017). XMLHttpRequest Specification: Living Standard. Retrieved from <https://xhr.spec.whatwg.org/#biblio-rfc2119>

Venners, B., &amp; Sommers, F. (2009). The Origins of Scala: A Conversation with Martin Odersky. Part I. Retrieved from <http://www.artima.com/scalazine/articles/origins\_of\_scala.html>

Waldo, J. (1998). Remote procedure calls and Java Remote Method Invocation. _IEEE Concurrency_, _6_(3). <https://doi.org/10.1109/4434.708248>

Waters, R. C. (1988). Program translation via abstraction and reimplementation. _IEEE Transactions on Software Engineering_, _14_(8), 1207–1228. <https://doi.org/10.1109/32.7629>

Yourgrau, P., &amp; Beginnen, K. (2005). _Gödel, Einstein und die Folgen: Vermächtnis einer ungewöhnlichen Freundschaft_. München: C.H. Beck.

Yuknewicz, P. (2014). Forum discussion: Bring back Classic Visual Basic, an improved version of VB6. Retrieved from <https://visualstudio.uservoice.com/forums/121579-visual-studio-2015/suggestions/3440221-bring-back-classic-visual-basic-an-improved-versi>

Yuknewicz, P., Latham, L., Onderka, P., &amp; Petrusha, R. (2016). Support Statement for Visual Basic 6.0 on Windows Vista, Windows Server 2008, Windows 7, Windows 8 and Windows 8.1, Windows Server 2012, Windows 10, and Windows Server 2016. Retrieved from <https://docs.microsoft.com/en-us/dotnet/visual-basic/reference/vb6-support>

Zaefferer, J., Balter, L., Willis, T., Tijhof, T., Resig, J., Greene, J. M.,. . . Partington, K. (2008). QUnit. GitHub. Retrieved from <https://github.com/qunitjs/qunit>

Zolciak, A. (2017). Progressive Web Applications: The Thing to Consider When Short on Resources. Retrieved from <https://insanelab.com/blog/web-development/progressive-web-apps-pwa-vs-native/>