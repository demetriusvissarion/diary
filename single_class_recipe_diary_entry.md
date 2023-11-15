# {{PROBLEM}} Class Design Recipe

## 1. Describe the Problem

_Put or write the user story here. Add any clarifying notes you might have._

## 2. Design the Class Interface

_Include the initializer, public properties, and public methods with all parameters, return values, and side-effects._

```python

class DiaryEntry:
    # Public Properties:
    #   title: a string
    #   contents: a string

    def __init__(self, title, contents): # title, contents are strings
        # Side-effects:
        #   Sets the title and contents properties
        pass

    def count_words(self):
        # Returns:
        #   An integer representing the number of words in the contents
        pass

    def reading_time(self, wpm):
        # Parameters:
        #   wpm: an integer representing the number of words the user can read
        #        per minute
        # Returns:
        #   An integer representing an estimate of the reading time in minutes
        #   for the contents at the given wpm.
        pass

    def reading_chunk(self, wpm, minutes):
        # Parameters:
        #   wpm: an integer representing the number of words the user can read
        #        per minute
        #   minutes: an integer representing the number of minutes the user has
        #            to read
        # Returns:
        #   A string representing a chunk of the contents that the user could
        #   read in the given number of minutes.
        # If called again, `reading_chunk` should return the next chunk,
        # skipping what has already been read, until the contents is fully read.
        # The next call after that it should restart from the beginning.
        pass
```

## 3. Create Examples as Tests

_Make a list of examples of how the class will behave in different situations._

``` python
import pytest
from lib.diary_entry import *

"""
Given an instance of the class with title / contents
#count_words Sets the title and contents properties (no return)
"""
def test_if_entry_added():
    diary_entry = DiaryEntry('15/11/2023 Gym', 'Completed upper body day 1 weightlifting program today')
    result = diary_entry.count_words()
    assert result == 10


"""
Given an instance of the class with title / contents
#reading_time returns reading time in minutes for the contents at the given wpm
"""
def test_if_calculates_reading_time():
    diary_entry = DiaryEntry('15/11/2023 Gym', 'Completed upper body day 1 weightlifting program today')
    result = diary_entry.reading_time(2)
    assert result == 4


"""
Given an instance of the class with title / contents
#reading_chunk returns a chunk of the contents that the user could read in the given number of minutes
"""
def test_if_can_read_chunk():
    diary_entry = DiaryEntry('15/11/2023 Gym', 'Completed upper body day 1 weightlifting program today')
    result = diary_entry.reading_chunk(2, 3)
    assert result == 'Completed upper body day 1 weightlifting'


"""
When class is instantiated without arguments
#count_words throws an error
"""
def test_if_throws_error_when_no_arguments():
    diary = DiaryEntry()
    with pytest.raises(Exception) as e: 
        result = diary.count_words()
    error_message = str(e.value)
    assert error_message == "No entry."
```

_Encode each example as a test. You can add to the above list as you go._

## 4. Implement the Behaviour

_After each test you write, follow the test-driving process of red, green, refactor to implement the behaviour._
