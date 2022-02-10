# Group-Making-AI #


This project was done as a part of CSCI-B-551 Elements of Artificial Intelligence Coursework under Prof. Dr. David Crandall.

## Command to run the program ##

python3 ./assign.py [input-file]

## State space ##
 All the states that can be generated upon shifting the conflicting members and the initial state with the minimum number of groups and every student is present in one of the groups.

## Initial state ##
 Initial state with the minimum number of groups and every student is present in one of the groups.

## Goal state ## 
No predefined goal state, goal is to minimize the overall cost of assigned groups.

## Successor state ##
Assign the most conflicting student in different permutations to minimize cost. 

## Cost function ## 
Cost of most conflicting student.

## Approach and design decisions ##

**Abstraction technique:** Local search

To begin with, we have created a method to read the input file. We have initialized a preferences dictionary for storing preferences of each student. We have also initialized a student’s list to store all the students. Moving forward, we have read the file containing all the student data by traversing through each line of the file. We have split each line by spaces to get all the answers entered by a student. We have retrieved the wanted team members by splitting it by ‘- ’ and getting the list of rest of the members. Then, we have calculated the number of team members that are required by the student. Now, we have checked if ‘zzz’ or ‘xxx’ is present in the wanted members list, if it is present, we have removed it. Now, we have retrieved the not wanted team members by splitting it with ‘,’ and then we have checked if ‘_’ is present in the not wanted members list, if it is not present, we have removed it. Now, we have added the student details to the dictionary and appended the student’s name to the students list. We have returned a tuple of preferences and students. Then we have found the most conflicting student i.e., the student with the most conflicting cost. For this we have iterated on every row and checked if the student is in that row finding the column in particular row and returning row and column as a tuple. Moving ahead we have calculated the cost of the assigned groups and the conflicting cost of each student. Then we have initialized a dictionary of conflicting cost with student name.  We have also initialised cost variable with number of groups multiplied by 5. Moving ahead we have  iterated through each group and through each student in the groups. Then we have checked if the group size is preference of student if not we are adding 2 to total cost and conflicting cost of each student. Then for each not wanted member is in the group if it’s there we are adding 10 to the total cost and conflicting cost for each conflicting members. Also, if any wanted member is in any group if it’s there, we are adding 3 to conflicting cost and total cost for each member. Moving ahead we have added the conflicting cost of student to conflicting list. We have returned a tuple of total cost and conflicting cost dictionary. 

We have created a method for getting the successor states depending on the conflicting student. We have initialized a successor groups list. Then we have iterated through each row for changing position of conflicting student, if the row has conflicting student, then we will make a deep copy of the current state and store it in the successor_group. Moving ahead we have popped off the element from the group and made a new group from it, if after popping, the group becomes empty then we are not taking new state as valid state, else if row didn’t have a conflicting student, we have iterated to each student in that group and swapped the conflicting student with each student and making all swaps as new state. We have made a deep copy of the current assignment, swapped the conflicting student and appended state into the successor groups list. If the length of the group is not 3, we will add the conflicting student to this group and make a new state. Then we have returned the successor groups. In the solver function we have parsed the input file to get the student preferences and name. Then we have initialized empty lists for assigning groups. Now, we have iterated through each student and put them into a group of three minimizing the assignment checking cost. Further, we have calculated the total cost and the conflicting cost of each student in the dictionary. We had set the total cost as the current cost to compare.  Then we have yielded the first assigned group and its cost. Now we have stored the conflicting costs by extracting the keys from the initial dictionary and then we have found the student with the maximum conflicting cost. If any other student has the same conflicting cost, we will assign it back to the dictionary. We have then calculated the time for the local cost. Now in a while loop, we have found the most conflicting student and then got all the successor states of the assigned group by changing position of most conflicting student. Now, iterating through each successor state, we have extracted the cost of successor and conflicting cost of students in successors state. We have then checked if the cost is less than current cost if yes, then yielding the new assigned group and cost. If the time of setting the most conflicting student is greater than 20, we have reinitialized the groups and taken the second most conflicting cost. If the time doesn’t reach 20, then we have checked the conflicting student from successor states.
