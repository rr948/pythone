Element Search Solutions
Exercise 20
Write a function that takes an ordered list of numbers (a list where the elements are in order from smallest to largest) and another number. The function decides whether or not the given number is inside the list and returns (then prints) an appropriate boolean.

Extras:

Use binary search.
Sample solution
There are two ways of solving this problem: one version using a simple for loop to search through the elements of a list, and one using the concept of binary search, looking at the elements in the most efficient way possible.

To use a simple for loop, a program will look like this:

# The exercise can be found at: http://www.practicepython.org/exercise/2014/11/11/20-element-search.html
#
# Write a function that takes an ordered list of numbers (a list where the elements are in order from smallest to largest) 
# and another number. The function decides whether or not the given number is inside the list and returns (then prints) 
# an appropriate boolean.

# find is a function that takes an ordered list of numbers and another number,
# returning true or false whether the element appears in the list
# 
# l is a list ordered from smallest to largest
# element is the number to find in the original list
def find(ordered_list, element_to_find):
  for element in ordered_list:
    if element == element_to_find:
      return True
  return False
  
if __name__=="__main__":
  l = [2, 4, 6, 8, 10]
  print(find(l, 5)) # prints False
  print(find(l, 10)) # prints True
  print(find(l, -1)) # prints False
  print(find(l, 2)) # prints True
view rawelement-search.py hosted with ❤ by GitHub
And to use binary search, one way of writing this program is like this:

# The exercise can be found at: http://www.practicepython.org/exercise/2014/11/11/20-element-search.html
#
# Write a function that takes an ordered list of numbers (a list where the elements are in order from smallest to largest) 
# and another number. The function decides whether or not the given number is inside the list and returns (then prints) 
# an appropriate boolean. THIS TIME, WITH THE EXTRA: USING BINARY SEARCH.

# find is a function that takes an ordered list of numbers and another number,
# returning true or false whether the element appears in the list
# 
# l is a list ordered from smallest to largest
# element is the number to find in the original list
def find(ordered_list, element_to_find):
  start_index = 1
  end_index = len(ordered_list) - 1
  
  while True:
    middle_index = (end_index - start_index) / 2
    
    if middle_index < start_index or middle_index > end_index or middle_index < 0:
      return False
    
    middle_element = ordered_list[middle_index]
    if middle_element == element_to_find:
      return True
    elif middle_element < element_to_find:
      end_index = middle_index
    else:
      start_index = middle_index
  
if __name__=="__main__":
  l = [2, 4, 6, 8, 10]
  print(find(l, 5)) # prints False
  print(find(l, 10)) # prints True
  print(find(l, -1)) # prints False
  print(find(l, 2)) # prints True
view rawelement-search-binary-search.py hosted with ❤ by GitHub
Note that there are many ways of implementing binary search correctly. One common technique is to use what is called “recursion” or “dynamic programming”, which calls a function from inside the function. What I have shown here is an example of binary search written with just the concepts of a while loop and if statements that we have seen before in this blog.