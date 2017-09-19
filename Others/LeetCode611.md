### Valid Triangle Number
- 给一堆数，有重复的，找出里面能凑成三角形边的组合个数。
- 1 先排个序，i循环0到length，j循环i到length，k循环j到length，这题也能算medium吗
- 2 看了solution，还有一种是二分查找来确定k的位置，看起来很灵性，但是复杂度并没有提高
- solution里说1的复杂度是`n*n`,我一开始以为是`n*n*n`,想了想最差情况下进行了`1+ 1+2+ 1+2+3+ ···· + 1+2+···+n`次，的确是`O(n*n)`
