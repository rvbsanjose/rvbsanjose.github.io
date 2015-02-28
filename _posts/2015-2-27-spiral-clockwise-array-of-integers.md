---
layout: post
title: Array of integers obtained by spiralling outward anti-clockwise from the r and c, starting upward
---

Recently, I found a great resource of toy problems on [GitHub](https://github.com/blakeembrey/code-problems/tree/master/problems) and wanted to take a stab at the following problem.

As a starting base to wrap my head around the problem and to see if I could spot any pattern, I used the whiteboard. What I found were two things.

Write a function that accepts four arguments. The first two arguments are the size of the grid (h x w), filled with ascending integers from left to right, top to bottom, starting from 1. The next two arguments are the starting positions, the row (r) and column (c).

Return an array of integers obtained by spiralling outward anti-clockwise from the r and c, starting upward.

    var spiral = function (h, w, r, c) {
      // value to start the board
      var begin = 1;
      var board = [];
      // build the board
      for (var i = 0; i < h; i++) {
      var row = [];
      while (row.length < w) { row.push(begin++); }
      board.push(row);
      }

      // run length for each direction
      var run = 1;
      // normalize the indexes
      var row = r - 1, col = c - 1;

      var positions = [];
      var recurse = function () {
      // if the length is equal, then we have visited all possibilities
      if (positions.length === h * w) { return; }
      // direction up
      for (var i = 0; i < run; i++) {
        if (board[row] && board[row][col]) { positions.push(board[row][col]); }
        row--;
      }
      // direction left
      if (positions.length === h * w) { return; }
      for (var i = 0; i < run; i++) {
        if (board[row] && board[row][col]) { positions.push(board[row][col]); }
        col--;
      }
      run++;
      // direction down
      if (positions.length === h * w) { return; }
      for (var i = 0; i < run; i++) {
        if (board[row] && board[row][col]) { positions.push(board[row][col]); }
        row++;
      }
      // direction right
      if (positions.length === h * w) { return; }
      for (var i = 0; i < run; i++) {
        if (board[row] && board[row][col]) { positions.push(board[row][col]); }
        col++;
      }
      run++;

      recurse();
      };

      recurse();
      return positions;
    };
