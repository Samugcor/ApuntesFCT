#apuntes #howto #codefragment #js 
___

```js
/**
 * Computes the shortest distance from point c to the segment ab
 * @param {Object} a - Starting point of the segment {x, y}
 * @param {Object} b - Ending point of the segment {x, y}
 * @param {Object} c - The point {x, y}
 * @returns {number} - The shortest distance
 */
function pointToSegmentDistance(a, b, c) {
  const abx = b.x - a.x;// X-component of vector AB
  const aby = b.y - a.y;
  const acx = c.x - a.x;
  const acy = c.y - a.y;

  const abSquared = abx * abx + aby * aby;

  // If a and b are the same point, return distance from c to a
  if (abSquared === 0) {
    const dx = c.x - a.x;
    const dy = c.y - a.y;
    return Math.sqrt(dx * dx + dy * dy);
  }

  // Compute the projection scalar t
  const t = ((acx * abx) + (acy * aby)) / abSquared;

  let closestPoint;
  if (t < 0) {
    // Closest to point a
    closestPoint = a;
  } else if (t > 1) {
    // Closest to point b
    closestPoint = b;
  } else {
    // Projection lies on the segment
    closestPoint = {
      x: a.x + t * abx,
      y: a.y + t * aby
    };
  }

  const dx = c.x - closestPoint.x;
  const dy = c.y - closestPoint.y;

  return Math.sqrt(dx * dx + dy * dy);
}

```