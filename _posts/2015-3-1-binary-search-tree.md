---
layout: post
title: Binary Search Tree
---

Implement a binarySearchTree class with the following properties:

* A .left property, a binary search tree (BST) where all values are lower than than it the current value.

* A .right property, a BST where all values are higher than than it the current value.

* A .insert() method, which accepts a value and places in the tree in the correct position.

* A .contains() method, which accepts a value and returns a boolean reflecting whether or not the value is contained in the tree.

* A .depthFirstLog() method, which accepts a callback and executes it on every value contained in the tree.

        var BinarySearchTree = function (value) {
          this.left;
          this.right;
          this.value = value;
        };

        BinarySearchTree.prototype.insert = function (value) {
          var newNode = new BinarySearchTree(value);
          var searchTree = function (node) {
            if (!node.left && node.value > value) {
              node.left = newNode;
            } else if (!node.right && node.value < value) {
              node.right = newNode;
            } else if (node.left && node.value > value) {
              searchTree(node.left);
            } else if (node.right && node.value < value) {
              searchTree(node.right);
            }
          };

          searchTree(this);
        };

        BinarySearchTree.prototype.contains = function (value) {
          var contains = false;
          var searchTree = function (node) {
            if (node.value === value) { contains = true; }
            if (!contains && node.left) { searchTree(node.left); }
            if (!contains && node.right) { searchTree(node.right); }
          };

          searchTree(this);
          return contains;
        };

        BinarySearchTree.prototype.depthFirstLog = function (cb) {
          var depthLog = function (node) {
            cb(node);

            if (node.left) { depthLog(node.left); }
            if (node.right) { depthLog(node.right); }
          };

          depthLog(this);
        };
