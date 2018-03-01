# Reliability
<p>In this assignment, you are asked to modify code that relates to a simple social networking concept: suggesting friends to a student based on who is taking the same classes.</p>

<p>The code works correctly but is susceptible to the types of issues discussed in the lesson on reliability, in particular unexpected inputs and mistakes made by the programmer who is using this code and the programmer whose code we are using. Your objective is to use defensive programming to make sure that the code does not throw any exceptions but still works correctly.</p>

<p>In completing this assignment, you will:</p>

<ul>
  <li>Apply defensive programming techniques to improve the reliability of code</li>
  <li>Get more experience understanding and modifying existing code</li>
</ul>

<p><b>Getting Started</b></p>

<p>Download the files that you will need for this assignment. In particular:</p>

<ul>
  <li><a href="//prod-edxapp.edx-cdn.org/assets/courseware/v1/c8f378d82a8763a0a18079d0a9c25130/asset-v1:PennX+SD2x+2T2017+type@asset+block/Student.java" target="[object Object]">Student.java</a> represents a student. For simplicity, the only field in this class is the student’s name.
  <li><a href="//prod-edxapp.edx-cdn.org/assets/courseware/v1/f8882ba777009ec6f0b3415c9fcc061d/asset-v1:PennX+SD2x+2T2017+type@asset+block/ClassesDataSource.java" target="[object Object]">ClassesDataSource.java</a> is an interface that defines a method called getClasses which returns a List containing the names of the classes being taken by the specified student.
  <li><a href="//prod-edxapp.edx-cdn.org/assets/courseware/v1/234856f21f67f215661f556ed6abac40/asset-v1:PennX+SD2x+2T2017+type@asset+block/StudentsDataSource.java" target="[object Object]">StudentsDataSource.java</a> is an interface that defines a method called getStudents which returns a List containing the Students who are taking the specified class
  <li><a href="//prod-edxapp.edx-cdn.org/assets/courseware/v1/c40d2ce08ae5a05f58cb4e01e2de20a4/asset-v1:PennX+SD2x+2T2017+type@asset+block/FriendFinder.java" target="[object Object]">FriendFinder.java</a> defines a method called findClassmates that works as described below. It relies on ClassesDataSource and StudentsDataSource.
</ul>

<p>The method takes a String representing the name of a student and then returns a Set containing the names of everyone else who is taking the same classes as that student. For instance, if the argument to the method represents me, and:</p>

<ul>
  <li>I am taking CIS573 and CIS550</li>
  <li>Alice is taking CIS573, CIS550, and CIS555</li>
  <li>Bob is taking CIS573 and CIS555</li>
  <li>Chen is taking CIS550 and CIS573</li>
  <li>Dhriti is taking CIS550</li>
</ul>

<p>then the method should return a Set containing Alice and Chen, since both of them are taking the same classes I am; however, it should not contain Bob or Dhriti since Bob is not taking CIS550 and Dan is not taking CIS573.</p>

<p><b>Activity</b></p>

<p>We will assume for our purposes that the FriendFinder.findClassmates method works correctly for good/valid inputs.</p>

<p>However, this code does not make any attempt to handle values that are null, including the input to the method, the objects on which it depends, and the objects that are returned from the methods it invokes. In any of these cases, the current code will throw a NullPointerException. Which is bad.</p>

<p>Using defensive programming, modify FriendFinder.findClassmates so that it does not throw any NullPointerExceptions in the situations listed above. Specifically:</p>

<ul>
  <li>Use IllegalArgumentException and IllegalStateException appropriately as discussed in the lesson</li>
  <li>Return null if the input Student is not taking any classes or if there are no students taking the same classes as that student</li>
  <li>Ignore any other null values encountered during the operation of the method</li>
  <li>You may not change the Student, StudentsDataSource, or ClassesDataSource code at all, nor should you change the FriendFinder constructor or the signature of FriendFinder.findClassmates. Likewise, you should not change that method’s behavior for good/valid inputs, but rather should only be looking for and handling null objects.</li>
</ul>

<p>Keep in mind that it is not sufficient to simply put a try/catch block around the entire method and catch any NullPointerException that arises, since in some cases the method must throw a different exception, in some cases it must return null, and in others it must simply ignore the null value and return the correct output.</p>

<p><b>Helpful Hints</b></p>

<p>Keep in mind that any object can be null, though if you use the “new” keyword you will not get a null object returned. But for all other objects in the code, check that they are not null before using them.</p>

<p>For testing your code, you may want to create your own implementations of the StudentsDataSource and ClassesDataSource interfaces and then have them return different values for the different things you are trying to protect against.</p>

<p><b>Before You Submit</b></p>

<p>Please be sure that:</p>

<ul>
  <li>your FriendFinder class is in the default package, i.e. there is no “package” declaration at the top of the source code</li>
  <li>your FriendFinder class compiles and you have not changed its constructor or the signature of the findClassmates method</li>
  <li>you have not created any additional .java files and have not made any changes to Student.java, StudentsDataSource.java, or ClassesDataSource.java (you do not need to submit these files)</li>
</ul>

<p><b>Assessment</b></p>

<p>Your submission will be assessed using automatic grading scripts that will check that the method works correctly and does not throw any exceptions for null values that it encounters. Your score is determined by the percentage of these tests that “pass,” i.e. that produce the correct result/behavior for the different situations when null values appear.</p>

<p>Before submitting your solution, you can run these grading scripts locally on your computer by following the steps below. These instructions assume you are using Eclipse, but should be applicable to other IDEs as well:</p>

<ol>
  <li>Download the JUnit distribution at junit-dist.jar and save it in your project's root directory. You should be able to do this by dragging it from Finder/Explorer into Eclipse and dropping it in the folder that has the same name as your project. Then add it to the project's build path by right-clicking the file name in Eclipse to get the pop-up/context menu, then selecting "Build Path -->" and then "Add to Build Path."</li>
  <li>Download the tests at homework10-tests.jar, and add it to the Eclipse project's build path as above.</li>
  <li>Now run the tests by right-clicking homework10-tests.jar in Eclipse to get the pop-up/context menu and selecting "Run As -->" and then "Java Application." You should see the tests run in the console and it should tell you your score for this assignment, or "Great job!" if your score would be 100%.</li>
</ol>

<p>Alternatively, if you would like to run the autograder from the command line, put the two .jar files and your .class file for this assignment in the same directory and run:</p>

<p><b>Mac/Linux:</b> java -cp .:junit-dist.jar:homework10-tests.jar Homework10Grader</p>

<p><b>Windows:</b> java -cp .;junit-dist.jar;homework10-tests.jar Homework10Grader</p>

<p>This will add junit-dist.jar and homework10-tests.jar to the classpath and then run Java with Homework10Grader as the main class.</p>
