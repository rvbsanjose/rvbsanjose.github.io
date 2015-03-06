---
layout: post
title: Finding the longest palindrome in a string
---

Implement a function that finds the longest palindrome in a given string. For example, in the string "My dad is a racecar athlete", the longest palindrome is "a racecar a". Count whitespaces as valid characters. Other palindromes in the above string include "dad", "ete", " dad " (including whitespace on each side of dad).

String "There was a tattarrattat on the racecar. It made a funny noise, gfedcbabcdefg" should return ' tattarrattat '

    var longestPalindrome = function (string) {
      var longest = '';
      for (var i = 0; i < string.length; i++) {
        // quick reference to the current letter in the string
        var currentLetter = string[i];
        // find the last occurance of the letter in the string
        var firstOccurance;
        for (var j = i + 1; j < string.length; j++) {
          if (currentLetter === string[j]) {
            // we found an occurance that matches the current letter
            firstOccurance = j;
            // generate the substring to match
            var subString = string.slice(i, firstOccurance + 1);
            // check if the substring is a palindrom and if it is longer then longest
            if (subString.length > longest.length &&
                subString.toLowerCase() === subString.split('').reverse().join('').toLowerCase()) {
                  longest = subString;
            }
          }
        }
      }
      // return the longest palindrome
      return longest;
    };
