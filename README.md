# Traveling salesman problem

This is my humble attempt of porting a C++ I [found on the internet][1] that `solves` the traveling salesman problem using the branch and bound algorithm.

### Usage

First, you need a cost matrix, being a two dimensional array of distances between nodes.

```typescript
const costMatrix: Matrix = [
  [Infinity, 10, 8, 9, 7],
  [10, Infinity, 10, 5, 6],
  [8, 10, Infinity, 8, 9],
  [9, 5, 8, Infinity, 6],
  [7, 6, 9, 6, Infinity],
];

const result = tsp.solve(costMatrix);

// Output:
{
   path: [ [ 0, 2 ], [ 2, 3 ], [ 3, 1 ], [ 1, 4 ], [ 4, 0 ] ],
   reducedMatrix: [
     [ Infinity, Infinity, Infinity, Infinity, Infinity ],
    [ Infinity, Infinity, Infinity, Infinity, Infinity ],
    [ Infinity, Infinity, Infinity, Infinity, Infinity ],
    [ Infinity, Infinity, Infinity, Infinity, Infinity ],
    [ Infinity, Infinity, Infinity, Infinity, Infinity ]
  ],
  level: 4,
  vertex: 4,
  cost: 34
}
```

Here, the output is a Node containing two valuable properties: `path` and `cost`.

The `path` property contain the indicies of the optimal/shortest route. The `cost` property is the total cost/distance of the tour.

### Geolocation

For convenience, a `geolocation` helper is built into this library.

```typescript
const points: tsp.Point[] = [
  // Buenos Aires - Argentina
  { type: 'Point', coordinates: [-58.435278, -34.606389] },
  // Rio de Janeiro - Brazil
  { type: 'Point', coordinates: [-43.277548, -22.875113] },
  // Santiago - Chile
  { type: 'Point', coordinates: [-70.666667, -33.45] },
  // Barcelona - Spain
  { type: 'Point', coordinates: [2.1741, 41.398371] },
  // Wellington - New Zeland
  { type: 'Point', coordinates: [174.783333, -41.3] },
  // Bang Rak - Thailand
  { type: 'Point', coordinates: [100.523884, 13.730579] },
  // Toronto - Canada
  { type: 'Point', coordinates: [-79.416667, 43.666667] },
];

// Output:
{
  path: [
    [ 0, 1 ], [ 1, 6 ],
    [ 6, 3 ], [ 3, 5 ],
    [ 5, 4 ], [ 4, 2 ],
    [ 2, 0 ]
  ],
  ...
  cost: 46544831.14534618 // in meters, 46.544 in kilometers
}
```

The first node is always the starting point, so you should put your point of departure first.

So, according to the result from above, the optimal tour would be:

|           From | To             |
| -------------: | -------------- |
|   Buenos Aires | Rio de Janeiro |
| Rio de Janeiro | Toronto        |
|        Toronto | Barcelona      |
|      Barcelona | Bang Rak       |
|       Bang Rak | Wellington     |
|     Wellington | Chile          |
|          Chile | Buenos Aires   |

And the cost would be around 46.544 kilometers

[1]: https://www.techiedelight.com/travelling-salesman-problem-using-branch-and-bound/
