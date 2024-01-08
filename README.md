This is the vector math and geometry library I've been slowly accreting for more than 30 years.  It's not that pretty, and it's not that clean, but it does a lot of what I need whenever I whip up a little graphics test.  I'm putting it in this repository to have a central copy.

Some functions and classes in this implementation and notes of interest:

* `vec2`, `vec3`, `vec4` - These expose the member array as `float*` so something like `v[0]` will work.
* `dot`, `min`, `max`, `length`, `normalize`, `reflect`, `refract`, and the normal math operators are all templated on the vector class (or any other class you'd like that defines `vector_size`)
* `rot4f` - Angle-axis rotation.  Notably `mult` and `operator*` concatenate rotations.
* `mat4f` - 4x4 matrix, including convenience functions `scale`, `translation`, `rotation`, `inverse`, `transpose`, `frustum` and `mult`
  * `inverse`  contains some very old code that inverts `mat4f` using Gaussian elimination.
* `vec4 operator*(const vec4& in, const mat4f& m)` multiplies a vector by a matrix.
* `make_plane` turns a vector and two vectors normal to the first vector into a "vector-distance" representation (useful for ray-plane intersection)
* `ray` can be transformed by a `mat4f`
* convenience functions `transform_ray` also transform a pair of origin and direction `vec3` by a matrix
* `aabox` can be constructed empty or from min and max `vec3`s, then extended with `vec3`s or more `aabox`s or spheres made of a `vec3` center and `float` radius.
* `add_sphere` extends a center and radius to enclose another center and radius.
* `range` encapsulates an interval that can be `intersect`ed with another `range`
* `ray_intersect_box` yields a `range` from a `ray` and `aabox`; the range may be `empty` indicating the `ray` didn't intersect the `aabox`.

