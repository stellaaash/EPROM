In mathematics, a vector **can represent either a position or a direction within a particular space**.
# Numerical Representation
Vectors can be represented both **geometrically**, but also **numerically**, through a sequence of numbers.
If a vector is in two-dimensions, it has two numbers. If it's in 3D, it has 3, etc.
Each of the numbers within a vector is called a *component*.
Each component usually has a name, for example the $x$, $y$ and $z$ components for a three-dimensional vector.
When written in text, vectors are represented with parenthesis, like so: (0, 2, 4), where 0 is $x$, 2 is $y$ and 4 is $z$.
In equations:

$$
\vec{a}
=
\begin{bmatrix}
x \\
y \\
z
\end{bmatrix}
$$ 
# Operations on Vectors
## Addition
Vector addition is *component-wise*.

$$
\vec{a} + \vec{b}
=
\begin{bmatrix}
a_x \\
a_y \\
a_z
\end{bmatrix}
+
\begin{bmatrix}
b_x \\
b_y \\
b_z
\end{bmatrix}
=
\begin{bmatrix}
a_x + b_x \\
a_y + b_y \\
a_z + b_z
\end{bmatrix}
$$
![Vector Addition](https://paroj.github.io/gltut/Basics/VectorAddition.svg)

Adding two vectors trailing each other reveals a result from the tail of the first vector to the head of the second.
![Vector Addition Head-to-Tail](https://paroj.github.io/gltut/Basics/VectorAdditionHeads.svg)

## Negation and Subtraction
You can negate a vector, which **reverses its direction**.
![Vector Negation](https://paroj.github.io/gltut/Basics/VectorNegation.svg)

$$
- \vec{a}
=
- \begin{bmatrix}
a_x \\
a_y \\
a_z
\end{bmatrix}
=
\begin{bmatrix}
-a_x \\
-a_y \\
-a_z
\end{bmatrix}
$$
___
As for vector subtraction, **it is the same as vector addition with the negation of the second vector**.
## Multiplication
Vector multiplication doesn't quite make sense geometrically, so we're left with just the numerical aspect instead.

$$
\vec{a} * \vec{b}
=
\begin{bmatrix}
a_x \\
a_y \\
a_z
\end{bmatrix}
*
\begin{bmatrix}
b_x \\
b_y \\
b_z
\end{bmatrix}
=
\begin{bmatrix}
a_x * b_x \\
a_y * b_y \\
a_z * b_z
\end{bmatrix}
$$
## Scalar Operations
Vectors can be operated on using [[Scalar]]s, which are just single numbers. 
Vectors can be added to a scalar, which has no geometric representation.

$$
s + \vec{a}
=
s
+
\begin{bmatrix}
a_x \\
a_y \\
a_z
\end{bmatrix}
=
\begin{bmatrix}
s + a_x \\
s + a_y \\
s + a_z
\end{bmatrix}
$$
___
Vectors can be multiplied by scalars, which **magnifies or shrink the length of the vector** depending on the scalar value.

$$
s * \vec{a}
=
s
*
\begin{bmatrix}
a_x \\
a_y \\
a_z
\end{bmatrix}
=
\begin{bmatrix}
s * a_x \\
s * a_y \\
s * a_z
\end{bmatrix}
$$

# Vector Length
The length of a vector is **its distance from its tail to its end geometrically**.
As for numerically, use this formula to get the exact distance:

$$
\lVert\vec{a}\rVert = \sqrt{a_x^2 + a_y^2 + a_z^2}
$$
This uses the [[Pythagorean Theorem]] to compute the length of the vector.
This also **works for any number of dimensions**, not just two or three.
# Unit Vectors and Normalization
A vector that has a length of exactly one is called a *unit vector*.
This represents a pure direction with a *standard, unit length*.
A unit vector variable in math equations is written with a `^` over the variable name.
A vector can be **converted into a unit vector by *normalizing* it**. This is done by **dividing the vector by its length**.
In other words, **multiplication by the [[Reciprocal]] of the length**.

$$
\hat{a}
=
\frac{1}{\lVert \vec{a} \rVert} * \vec{a}
=
\begin{bmatrix}
\frac{a_x}{\lVert \vec{a} \rVert} \\
\frac{a_y}{\lVert \vec{a} \rVert} \\
\frac{a_z}{\lVert \vec{a} \rVert}
\end{bmatrix}
$$
