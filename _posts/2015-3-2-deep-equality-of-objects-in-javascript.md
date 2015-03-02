---
layout: post
title: Deep equality of objects in JavaScript
---

Write a function that, given two objects, returns whether or not the two are deeply equivalent--meaning the structure of the two objects is the same, and so is the structure of each of their corresponding descendants. Don't worry about handling cyclical object structures.

Examples:

* deepEquals({a:1, b: {c:3}},{a:1, b: {c:3}}); // true
* deepEquals({a:1, b: {c:5}},{a:1, b: {c:6}}); // false

        var deepEquals = function (apple, orange) {
          var objType = function (obj) {
            return Object.prototype.toString.call(obj) === '[object Object]';
          };

          for (var key in apple) {
            // if the key doesn't exist in the other obj, then it's not deeply equal
            if (!orange[key]) { return false; }
            // if both are not obj's and values do not exist, it's not deeply equal
            if (!objType(apple[key]) && !objType(orange[key]) && apple[key] !== orange[key]) {
              return false;
            }
            // if both params are obj's, then recurse
            if (objType(apple[key]) && objType(orange[key])) {
              var resp = deepEquals(apple[key], orange[key]);
              if (!resp) { return false; }
            }
          }

          // it must be deeply equal
          return true;
        };
