---
layout: post
title: Resizing a hash table
---


Create a hash table with `insert()`, `retrieve()`, and `remove()` methods.

* Be sure to handle hashing collisions correctly.
* Set your hash table up to double the storage limit as soon as the total number of items stored is greater than 3/4th of the number of slots in the storage array.
* Resize by half whenever utilization drops below 1/4.

        var makeHashTable = function(){
          var result = {};
          var storage = [];
          var storageLimit = 4;
          var size = 0;
          result.insert = function(key, value){
            // TODO: implement `insert`
            size++;
            var index = getIndexBelowMaxForKey(key, storageLimit);
            var bucket = storage[index];
            if (bucket) {
              // check if value is already in the bucket and update it
              for (var i = 0; i < bucket.length; i++) {
                if (bucket[i][0] === key) {
                  bucket[i][1] = value;
                }
              }
              // the value is not in the bucket so just insert it
              bucket.push([key, value]);
            } else {
              // no bucket at the storage location
              storage[index] = [];
              storage[index].push([key, value]);
            }
            if (size / storageLimit >= 0.75) {
              result.resize(storageLimit * 2);
            }
          };

          result.retrieve = function(key){
            // TODO: implement `retrieve`
            var index = getIndexBelowMaxForKey(key, storageLimit);
            var bucket = storage[index];
            if (bucket) {
              for (var i = 0; i < bucket.length; i++) {
                // Does the value match
                if (bucket[i][0] === key) {
                  // We have found the value in the bucket
                  return bucket[i][1];
                }
              }
            }

            return undefined;
          };

          result.remove = function(key){
            // TODO: implement `remove`
            var index = getIndexBelowMaxForKey(key, storageLimit);
            var bucket = storage[index];
            if (bucket) {
              for (var i = 0; i < bucket.length; i++) {
                if (bucket[i][0] === key) {
                  // Found the value so decrease size by 1
                  size--;
                  bucket.splice(i, 1);
                }
              }
            }
            if (size / storageLimit <= 0.25) {
              result.resize(storageLimit / 2);
            }
          };

          result.resize = function (newLimit) {
            // Keep a reference to the storage to reset it
            var oldStorage = storage;
            // Update the size limit of the storage
            storageLimit = newLimit;
            // Clear the storage
            storage = [];

            // Go thru each bucket in the storage
            for (var i = 0; i < oldStorage.length; i++) {
              var bucket = oldStorage[i];
              if (bucket) {
                // Reassign for each bucket
                for (var j = 0; j < bucket.length; j++) {
                  var index = getIndexBelowMaxForKey(bucket[j][0], storageLimit);
                  var newBucket = storage[index];
                  if (newBucket) {
                    newBucket.push([bucket[j][0], bucket[j][1]]);
                  } else {
                    newBucket = [];
                    newBucket.push([bucket[j][0], bucket[j][1]]);
                  }
                }
              }
            }
          };

          return result;
        };

        // This is a "hashing function". You don't need to worry about it, just use it
        // to turn any string into an integer that is well-distributed between
        // 0 and max - 1
        var getIndexBelowMaxForKey = function(str, max){
          var hash = 0;
          for (var i = 0; i < str.length; i++) {
            hash = (hash<<5) + hash + str.charCodeAt(i);
            hash = hash & hash; // Convert to 32bit integer
            hash = Math.abs(hash);
          }
          return hash % max;
        };
