# CS350-Homework-7-solved

Download Here: [CS350 Homework #7 solved](https://jarviscodinghub.com/assignment/homework-7-solution/)

For Custom/Original Work email jarviscodinghub@gmail.com/whatsapp +1(541)423-7793

Read this short primer about multithreading in Java. Using multithreading you are able to have multiple threads (for our purposes, we can also think of them as processes as well).

Write a Java program that will spawn and run concurrently two threads of the same code. The code that each thread will follow should consist of a loop that executes five times. Each iteration of the loop should start by having the thread print the first of the five lines below (using a “print” statement), then sleep for some random amount of time (say between 0 and 20 msec), then print the second line, then sleep again, etc. until all five lines below are printed out.
“Thread i is starting iteration k”

“We hold these truths to be self-evident, that all men are created equal,”

“that they are endowed by their Creator with certain unalienable Rights,”

“that among these are Life, Liberty and the pursuit of Happiness.”

“Thread i is done with iteration k”

Run your code and show that the output of the two processes will be interleaved (making the output incomprehensible).

To make the above work, you will need to use a critical section so that the five print statements in a single iteration are all inside that critical section. Use the following version of the Dekker’s algorithm and show that the statements are printed cohesively.
CS Entry Protocol for Procedss i
flag[i]:=true;
while flag[j]{
if (turn==j) {
flag[i]:=false;
while (flag[j]==true) {};
flag[i]:=true;
}
}

CS Exit Protocol for Process i
turn:=j;
flag[i]:=false;

Can you illustrate (using your code) that using the above Dekker algorithm, it is possible for (say) thread 0 to be executing its entry protocol while thread 1 manages to get into the critical section more than once.Hint: You may want to use artificial delay (e.g., sleep) instructions that will make the threads proceed at different speeds.

Replace the above Dekker algorithm with the following Peterson algorithm and show that the scenario you created in (c) does not occur.
CS Entry Protocol for Process i
turn:=j;
flag[i]:=true;
while (flag[j] && turn==j) {};

CS Exit Protocol for Process i
flag[i]:=false;

Consider the Bakery algorithm discussed in class and in the notes. One idea was to use a ticket = 1 to avoid having to use the “choosing” flag. Making such a change would give us the code below.
Note: Assume that the variable ticket can be arbitrarily large (i.e., you do not have to worry about it becoming too big).
CS Entry Protocol for Process i
ticket[i]:=1;
ticket[i]:=max(ticket[0]..ticket[n-1])+1;
for j:=0 to n-1 do {
while(ticket[j]!=0 && (ticket[j],j)<(ticket[i],i)){};
}

CS ExitProtocol for Process i
ticket[i]:=0;

Does the above tweak work? If yes, then prove it, if not, then provide a counter example.
Implement the above version of the Bakery algorithm in Java, and dependent on your answer to part (a) either show a set of (say 4) threads reciting the declaration of independence cohesively, or else not.

As discussed in class, all software approaches for mutual exclusion rely on “busy waiting”. In this problem, we will “measure” the overhead from this busy waiting. We will do so simply by counting the number of times a busy waiting loop is executed in your solution of problem (1.d). You can do so by having each thread keep a count of how many times it executed the “while” loop. What results do you obtain? e.g., on average, how many times is the busy-waiting loop executed per request for the critical section? You may want to repeat your experiment a number of times and report a 95th-percent confidence interval.
Note: By incrementing a counter in the busy-waiting loop, you are effectively undercounting the number of iterations — i.e., without that counter in the picture, the loop condition would have been checked more times.
