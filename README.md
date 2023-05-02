Download Link: https://assignmentchef.com/product/solved-cmpt280-assignment-1-linked-list-classes-from-the-data-structure-library-lib280
<br>
For this assignment you’ll be working with linked list classes from the data structure library lib280. lib280 is a library of data structures that we will build up over the duration of the course. We will start with a version of lib280 that has very few data structures in it and add more with each assignment. Each assignment will come with a new version of lib280 which contains the correct implementations of ADTs that were the subject of the previous assignment.

Obtaining and Setting Up lib280

For this assignment the first thing you’ll need to do is to obtain a copy of lib280-asn1. It is provided along with this assignment description on the class webpage. Download the lib280-asn1.zip file and expand its contents somewhere in your filesystem.

The class website provides a self-guided tutorial that explains how to import lib280 into an IntelliJ project once you have downloaded it; it is located under the “Laboratory/Tutorial Resources” heading. First complete part 1 of the tutorial to create an empty IntelliJ project. Then complete part 2 of the tutorial to import lib280-asn1 into your project. For question 1 complete part 3 of the tutorial to create a module for your program that can use the classes from lib280-asn1. For questions 2 and 3 you don’t need to complete part 3 again because you’ll just be working within the lib280-asn1 module.

Navigating lib280-asn1 Within IntelliJ

The lib280-asn1 module contains several packages. The classes of interest to use for this assignment are in the lib280.list package. Find the lib280-asn1 module in your “project” tab, normally located on the left side of the IntelliJ window. Expand it by clicking the little triangle beside it. This should reveal a folder called “src”. Expand that as well. Now you will see a list of java packages that contain the various classes in the lib280-asn1 library. For this assignment, the classes we are interested in are in the lib280.list package, so click the triangle to expand it. You should now see classes like LinkedList280 and BilinkedList280.

Singly- and Doubly- Linked List Classes in lib280

The UML diagram below shows the class hierarchy you’ll be working with in this assignment. It may look a bit daunting at first, but you’ll soon see it’s not that complicated. There are four pairs of classes/interfaces (surrounded by light blue boxes<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>). In each pair, there is one class for a singly-linked list and one for a doubly-linked list. The class/interface of each pair that pertains to doubly linked lists extends the class/interface related to singly linked lists.

LinkedNode280&lt;I&gt;<strong>: </strong>The node class used for a singly-linked list.

BilinkedNode280&lt;I&gt;<strong>: </strong>An extension of LinkedNode280&lt;I&gt; that adds the “previous node” reference required for nodes in a doubly linked list.

LinearIterator280&lt;I&gt;<strong>: </strong>An interface that defines the methods that must be supported by cursors and iterators that can step forwards over a linear structure, such as goFirst(), goForth(), after(), etc.

BilinearIterator280&lt;I&gt;<strong>: </strong>An interface that extends LinearIterator280&lt;I&gt; by adding methods that allow stepping backwards, such as goBack() and goLast().

LinkedIterator&lt;I&gt;<strong>: </strong>An implementation of LinearIterator280&lt;I&gt; which is an iterator object for a singlylinked list. It is used by the LinkedList280&lt;I&gt; class to provide iterators.

BiinkedIterator&lt;I&gt;<strong>: </strong>An implementation of BilinearIterator280&lt;I&gt;, and an extension of LinkedIterator280&lt;I&gt;, which is an iterator object for a doubly-linked list. It is used by the BilinkedList280&lt;I&gt; class to provide iterators.

LinkedList280&lt;I&gt;<strong>: </strong>A singly-linked list class. It provides a cursor by implementing the LinearIterator280&lt;I&gt; interface. The Nodes of the list are LinkedNode280&lt;I&gt; objects, and it can provide iterators of of type LinkedIterator&lt;I&gt;.

BiLinkedList280&lt;I&gt;<strong>: </strong>A doubly-linked list class. It provides a cursor that can move both forwards and backwards by implementing the BilinearIterator280&lt;I&gt; interface. The nodes of the list are BilinkedNode280&lt;I&gt; objects, and it can provide iterators of of type BilinkedIterator&lt;I&gt;.

Take a moment to familiarize yourself with these classes and their methods, particularly the LinkedList280&lt;I&gt; and LinkedIterator280&lt;I&gt; classes as you will be working on coding extensions of these classes.

<h2><img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/06/449.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/06/449.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>Iterators</h2>

This section describes a bit more about how iterators work. Iterators provide the same functionality as a container ADT that has a cursor, but they are separate objects from the container. This allows us to record a cursor position that is different and independent from the position recorded by the container’s internal cursor.

The list objects, LinkedList280&lt;I&gt; and BilinkedList280&lt;I&gt; both have methods called iterator. The iterator method in the LinkedList280&lt;I&gt; class returns a new cursor position encapsulated in an instance of the LinkedIterator280&lt;I&gt; class. This instance will have references directly to the nodes of the LinkedList280&lt;I&gt; instance that created it. In essence, the LinkedIterator280&lt;I&gt; contains its own copies of the position and prevPosition fields that appear in LinkedList280&lt;I&gt; – i.e. another cursor that is external to the list! This cursor can be manipulated in exactly the same was as the internal cursor of the list. If you compare the methods in LinkedIterator280&lt;I&gt; to the methods of the same name in LinkedList280&lt;I&gt;, you’ll see that they are almost identical.

Thus, each time we want a new cursor that is independent of the list’s internal cursor, we can call the iterator method and get a new one. This adds additional flexibility. If we can get away with just using the lists internal cursor for our purposes, then we can do so, but we have the option to create more cursors in the form of iterators should we so desire.

<h1>3      Your Tasks</h1>

<strong>Question 1 (9 points):</strong>

Tractor Jack is a notorious pirate captain who sails the Saskatchewan River plundering farms for wheat, barley, and all the other grains. You may remember him from his exploits in CMPT 141.<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a>

Jack employs the members of his pirate crew at ten different ranks (numbered 0 through 9). A crew member’s rank is generally related to the number of sacks of grain they are able to plunder annually. Although there is some variability, Jack is certain that pirates of higher rank generally plunder more sacks of grain than those he appoints at lower ranks. As such, jack generally pays pirates of higher rank more than than pirates of lower rank (though each pirate’s pay is negotiated separately, so every crew member has a different annual salary).

Jack has always negotiated crew member pay based on his gut feeling, which is perhaps a poor way of doing “business”. He wants to analyze his payroll to see if the annual salaries of his crew members are equitable in the sense that he’d like his crew members at each rank to be paid about the same <strong>per sack of grain </strong>that they plunder.

You will write a program to determine the total amount Jack paid his crew <strong>per sack of grain </strong>for each crew rank separately. If the amount paid per sack of grain plundered varies a lot over the different ranks, Jack may want to re-think his pay scale and his negotiation tactics.

In the provided file PerformanceByRank.java you are given code that reads a data file piratecrew.txt (provided) containing the pay data for all of Jack’s crew. The data will be returned as a linked list of Crew objects of type LinkedList280&lt;Crew&gt;. A Crew object contains the rank, annual pay (in golden guineas), and the number of sacks of grain plundered in the last year by a crew member. It has getters and setters for each of these three pieces of data. Crew.java defining this class is provided.

In the main() function of PerformanceByRank.java, write a program that does the following:

<ol>

 <li>Create an array piratesByRank of ten LinkedList280&lt;Crew&gt; objects, one for each rank (you saw how to do this in Tutorial 1).</li>

 <li>Initialize the elements of the array of linked lists piratesByRank.</li>

 <li>Iterate through the list of Crew objects returned by readCrewData() and add each Crew object to the list at offset r of piratesByRank, where r is the crew member’s rank.</li>

 <li>For each list, determine the amount paid to all of the crew members of that rank <strong>per sack of grain plundered by all of the crew members of that rank </strong>and print it to the console (see the sample output section, below). If a list is empty, instead print to the console a message that Jack has no pirates employed at that rank.</li>

</ol>

<strong>You are not permitted to modify any of the provided code. Exception: you are allowed to modify the pathname to the input file </strong>piratecrew.txt <strong>in the event that you get a “file not found” error.</strong>

<h2>Sample Output</h2>

Jack’s rank 0 crew members were paid of 2000.0 guineas per sack of grain plundered.

Jack’s rank 1 crew members were paid of 258.78087720909235 guineas per sack of grain plundered.

Jack’s rank 2 crew members were paid of 252.1541797737082 guineas per sack of grain plundered.

Jack’s rank 3 crew members were paid of 274.9021704266409 guineas per sack of grain plundered. Jack’s rank 4 crew members were paid of 317.725137629488 guineas per sack of grain plundered.

Jack’s rank 5 crew members were paid of 339.7282378647562 guineas per sack of grain plundered.

Jack’s rank 6 crew members were paid of 360.94124515527716 guineas per sack of grain plundered.

Jack’s rank 7 crew members were paid of 386.91136146494415 guineas per sack of grain plundered.

Jack’s rank 8 crew members were paid of 398.8308541852052 guineas per sack of grain plundered.

Jack’s rank 9 crew members were paid of 436.2818307435587 guineas per sack of grain plundered.

<strong>Question 2 (20 points):</strong>

The BilinkedList280&lt;I&gt; and BilinkedIterator280&lt;I&gt; classes in lib280-asn1 are incomplete. There are missing method bodies in each class. Each missing method body is tagged with a // TODO comment. The javadoc headers for each method explain what each method is supposed to do<a href="#_ftn3" name="_ftnref3"><sup>[3]</sup></a>. Many of the methods you must implement override methods of the LinkedList280&lt;I&gt; superclass. Add your code right into the existing files within the lib280-asn1 module.

When implementing the methods, consider carefully any special cases that might cause need to update the cursor position, or ensure that it remains in a valid state.

<strong>You are not permitted to modify any existing code in the .java files given. You may only fill in the missing method bodies.</strong>

<strong>Question 3</strong>

Write a regression tests for the BilinkedList280&lt;I&gt; class. You only need to test the methods that <em>you </em>had to write. You may generate test cases using white-box, black-box, or a combination of both methods. Again, write this code in the existing BiLinkedList280.java within the lib280-asn1 project. A function header for the regression test (main() function) has already been provided.

Marks for this question will be earned for generating and coding good tests, not whether or not the methods being tested actually work. This means that you can still get full marks on this question even if the methods you were supposed to code in Question 2 don’t work.

<a href="#_ftnref1" name="_ftn1">[1]</a> The light blue boxes in the UML diagram are only to show the pairs of classes that serve the same roles for singly-/doubly-linked lists and do not represent any actual grouping within lib280. All of the pictured classes are in the same package within lib280.

<a href="#_ftnref2" name="_ftn2">[2]</a> This question was inspired by <a href="https://www.youtube.com/watch?v=DuGGNsE3_8Y">this song (click to link)</a><a href="https://www.youtube.com/watch?v=DuGGNsE3_8Y">.</a> Arrrr!

<a href="#_ftnref3" name="_ftn3">[3]</a> The javadoc comments in these files are also good examples of how we will expect you to document methods that you write yourself in future assignments.