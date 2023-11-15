# {{PROBLEM}} Class Design Recipe

## 1. Describe the Problem

_Put or write the user story here. Add any clarifying notes you might have._

## 2. Design the Class Interface

_Include the initializer, public properties, and public methods with all parameters, return values, and side-effects._

```python

import math

class Diary:
    def __init__(self):
        pass

    def add(self, entry):
        # Parameters:
        #   entry: an instance of DiaryEntry
        # Returns:
        #   Nothing
        # Side-effects:
        #   Adds the entry to the entries list

        # turn the two strings in one string called "entry" with format "title: contents"
        # store each "entry" in a list_of_entries
        pass

    def all(self):
        # 
        # raise Exception("Invalid text, must have at least one character.")
        # Returns:
        #   A list of instances of DiaryEntry

        # print each "entry" consecutively on separate rows 
        pass

    def count_words(self):
        # Returns:
        #   An integer representing the number of words in all diary entries
        # HINT:
        #   This method should make use of the `count_words` method on DiaryEntry.

        # create a dictionary "words_count" to store "title": "number_of_words" (helps for later stages)
        # return the sum of the values from "words_count"
        pass

    def reading_time(self, wpm):
        # Parameters:
        #   wpm: an integer representing the number of words the user can read
        #        per minute
        # Returns:
        #   An integer representing an estimate of the reading time in minutes
        #   if the user were to read all entries in the diary.

        # result = math.ceil(self.count_words() / wpm)
        # return result
        pass

    def find_best_entry_for_reading_time(self, wpm, minutes):
        # Parameters:
        #   wpm:     an integer representing the number of words the user can
        #            read per minute
        #   minutes: an integer representing the number of minutes the user has
        #            to read
        # Returns:
        #   An instance of DiaryEntry representing the entry that is closest to,
        #   but not over, the length that the user could read in the minutes
        #   they have available given their reading speed.

        # can_read = wpm * minutes
        # build list of all values from "words_count"
        # iterate through that list and find the number that is closest to, but not over (see below code)
        # 
        pass
```

## 3. Create Examples as Tests

_Make a list of examples of how the class will behave in different situations._

Note: all tests for this Diary class will be integration tests as every method uses the DiaryEntry class

``` python

import pytest
from lib.diary import *
from lib.diary_entry import *
"""
Given an instance of DiaryEntry
#add Adds the entry to the entries list
"""
def test_if_entry_added():
    diary_entry = DiaryEntry('15/11/2023 Gym', 'Completed upper body day 1 weightlifting program today')
    diary = Diary()
    diary.add(diary_entry)
    result = diary.all()
    assert result == '15/11/2023 Gym: Completed upper body day 1 weightlifting program today'


"""
When all() function is called after adding entries
#all returns a list of all entries
"""
def test_if_shows_all_entries():
    diary_entry1 = DiaryEntry('14/11/2023 Gym', 'Completed upper body day 1 weightlifting program today')
    diary_entry2 = DiaryEntry('15/11/2023 Gym', 'Completed upper body day 2 weightlifting program today')
    diary = Diary()
    diary.add(diary_entry1)
    diary.add(diary_entry2)
    result = diary.all()
    assert result == '14/11/2023 Gym: Completed upper body day 1 weightlifting program today \n15/11/2023 Gym: Completed upper body day 2 weightlifting program today \n'


"""
When count_words() function is called after adding entries
#count_words returns an integer representing the number of words in all diary entries
"""
def test_if_counts_words_in_all_entries():
    diary_entry1 = DiaryEntry('14/11/2023 Gym', 'Completed upper body day 1 weightlifting program today')
    diary_entry2 = DiaryEntry('15/11/2023 Gym', 'Completed upper body day 2 weightlifting program today')
    diary = Diary()
    diary.add(diary_entry1)
    diary.add(diary_entry2)
    result = diary.count_words()
    assert result == 20


"""
When reading_time() function is called after adding entries
#reading_time returns an integer of reading time in minutes if user reads all entries
"""
def test_if_calculates_reading_time():
    diary_entry1 = DiaryEntry('14/11/2023 Gym', 'Completed upper body day 1 weightlifting program today')
    diary_entry2 = DiaryEntry('15/11/2023 Gym', 'Completed upper body day 2 weightlifting program today')
    diary = Diary()
    diary.add(diary_entry1)
    diary.add(diary_entry2)
    result = diary.reading_time(2)
    assert result == 10


"""
When find_best_entry_for_reading_time() function is called after adding entries
#find_best_entry_for_reading_time returns best entry to read
"""
def test_if_finds_best_entry_for_reading_time():
    diary_entry1 = DiaryEntry('14/11/2023 Gym', 'Completed upper body day 1 weightlifting program today')
    diary_entry2 = DiaryEntry('15/11/2023 Latin Lesson', 'Suspendisse pretium gravida commodo. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Sed cursus commodo lacus, vitae efficitur dolor. Aliquam sit amet volutpat magna. Morbi dapibus lorem at turpis luctus imperdiet. Mauris pharetra diam urna, vitae molestie lectus auctor ut. Proin iaculis lacus id augue elementum, sed ullamcorper nibh pharetra. Suspendisse ac ex orci.')
    diary = Diary()
    diary.add(diary_entry1)
    diary.add(diary_entry2)
    result = diary.find_best_entry_for_reading_time(2, 5)
    assert result == '14/11/2023 Gym: Completed upper body day 1 weightlifting program today'



"""
When all() function is called without adding entries
#all throws an error
"""
def test_throws_error_when_no_entries():
    diary = Diary()
    with pytest.raises(Exception) as e: 
        result = diary.all()
    error_message = str(e.value)
    assert error_message == "No entry."
# raises an error with the message "No entry."
```

_Encode each example as a test. You can add to the above list as you go._

## 4. Implement the Behaviour

_After each test you write, follow the test-driving process of red, green, refactor to implement the behaviour._
