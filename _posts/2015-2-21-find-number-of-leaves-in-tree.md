---
layout: post
title: Finding the number of leaves in a tree
---

Finding the number of leaves in a tree can be represented by the nodes within a tree that have no children.

         * <- root
        / \
       *    * <- leaf
      / \
     *   * <- leaf

To further illustrate this, below is an example of a constructor function for the tree. For every instance of a new tree a property of children is initialize as an empty array.

var Tree = function (value) {
  this.value = value;
  this.children = [];
};

Let’s start by defining a countLeaves method on the Tree prototype. As mentioned earlier, a leaf is a node that has no children. Since a instance of a tree has a children property that is an array, it’s as simple as recursing through the tree and checking the length of the children. The example below, is using the DFS (Depth First Search) strategy.

Tree.prototype.countLeaves = function () {
  var leaves = 0;

  if (!this.children.length) return 1;
  var countLeaves = function (node) {
    if (!node.children.length) { leaves++; }
    for (var i = 0; i < node.children.length; i++) {
      var child = node.children[i];
      countLeaves(child);
    }
  };

  countLeaves(this);
  return leaves;
};
