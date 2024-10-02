---
icon: chart-scatter-3d
description: >-
  This chapter will explain what coordinate transformations are, and how they
  are useful in Materials Science.
---

# Coordinate Transformations

## Coordinate Axis

What are coordinates? They are a set of predetermined directions that allow us to navigate space and use direction meaningfully. These directions are orthogonal to one another and can be determined arbitrarily. These axii can have many labeling conventions. Commonly, you will see a coordinate axis labeled X, Y, and Z.&#x20;

<figure><img src="https://d138zd1ktt9iqe.cloudfront.net/media/seo_landing_files/sagar-a-cartesian-coordinate-07-1604485189.png" alt=""><figcaption><p>An example coordinate axis</p></figcaption></figure>

There are some rules that these arbitrary directions must follow by engineering convention. As stated, the 3 directions must be mutually orthogonal, meaning the angle between each direction is 90 degrees. The axis must also follow what is known as, "The Right Hand Rule".&#x20;

<figure><img src="https://bobcad.com/wp-content/uploads/2019/05/image-1-right-hand-rule.png" alt=""><figcaption><p>Illustration of the right hand rule. (from bobcad.com)</p></figcaption></figure>

This means that your X direction crossed (a vector math operation) with your Y direction will equal the positive Z direction. This is important to maintain uniformity across researchers. Many physical phenomena follow this "Right Hand Rule" convention, such as the direction of magnetic field with respect to current flowing through a wire.&#x20;

## Developing a Transformation Matrix

Transforming a coordinate axis is actually quite simple when thought about in the right framework. These "axis" are nothing but vectors in 3-D space situated mutually orthogonal to one another. Therefore, when transforming to a new axis, one needs to simply express the new coordinates in terms of vector addition from the old coordinates. The "New X" is simply a vector addition of the "Old X, Y and Z". In other words, this new direction is " \_\_\_\_ of the Old X, plus \_\_\_\_ of the Old Y, plus \_\_\_\_ of the Old Z" where the blanks represent a scaling factor. In the below image, the faded coordinate system: a1, a2, and a3, is known as the parent frame. The bolded coordinate system: b1, b2, and b3, is known as the child frame.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>An example of a coordinate transformation. (modified from <a href="https://dugas.ch/transform_viewer/index.html">https://dugas.ch/transform_viewer/index.html</a>)</p></figcaption></figure>

$$
\left[\begin{matrix} {a_1 \cdot b_1} & {a_2 \cdot b_1} & {a_3 \cdot b_1} \\ {a_1 \cdot b_2} & {a_2 \cdot b_2} & {a_3 \cdot b_2} \\ {a_1 \cdot b_3} & {a_2 \cdot b_3} & {a_3 \cdot b_3} \end{matrix}\right]
$$

This is a matrix representation of the idea described above. The top row of the matrix can be thought of as "the contribution of a1 onto b1, the contribution of a2 onto b1, and the contribution of a3 onto b1" Using that top row, the new coordinate direction, "b1" can be found using the previous 3 coordinate axis. This process then needs to be repeated for "b2" and "b3". This general process can be used to develop a "transformation matrix" between any 2 coordinate axii. To develop this matrix, angles between the new and old axii, and their cosines, will be used.&#x20;

$$
\left[\begin{matrix} 
a_1 \cdot b_1 & a_2 \cdot b_1 & a_3 \cdot b_1 \\ 
a_1 \cdot b_2 & a_2 \cdot b_2 & a_3 \cdot b_2 \\ 
a_1 \cdot b_3 & a_2 \cdot b_3 & a_3 \cdot b_3 
\end{matrix}\right]
\cdot
\left[\begin{matrix} 
a_1 \\ 
a_2 \\ 
a_3 
\end{matrix}\right]
$$



We can use this transformation matrix, which we can call R, to transform any vector in the a-frame (or parent frame) to a vector in the b-frame (or child frame).

$$
\left[ \begin{matrix} b_1 \\ b_2 \\ b_3 \end {matrix}\right] = \left[\begin{matrix} 
a_1 \cdot b_1 & a_2 \cdot b_1 & a_3 \cdot b_1 \\ 
a_1 \cdot b_2 & a_2 \cdot b_2 & a_3 \cdot b_2 \\ 
a_1 \cdot b_3 & a_2 \cdot b_3 & a_3 \cdot b_3 
\end{matrix}\right]
\cdot
\left[\begin{matrix} 
a_1 \\ 
a_2 \\ 
a_3 
\end{matrix}\right]
$$

### A Simple Example

To better understand the concept of a coordinate transformation, let's try a simple example problem. To simplify the problem, we can consider a coordinate transformation in 2-dimensions.&#x20;

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption><p>An example of a 2-D coordinate transformation.</p></figcaption></figure>

In this scenario, we need a transformation matrix that will map a1 and a2 onto b1, and map a1 and a2 onto b2.&#x20;

$$
\left[ \begin{matrix} b_1 \\ b_2 \end {matrix}\right] = \left[\begin{matrix} 
a_1 \cdot b_1 & a_2 \cdot b_1 \\ 
a_1 \cdot b_2 & a_2 \cdot b_2 \end{matrix}\right]
\cdot
\left[\begin{matrix} 
a_1 \\ 
a_2 
\end{matrix}\right]
$$

To fill out our transformation matrix, we simply need to find the cosine of the angle between the parent coordinates and the child coordinates. Let's start with a1 onto b1 and a2 onto b1.

$$
a_1 \cdot b_1 = \cos(30)
$$

$$
a_2 \cdot b_1 = \cos(60)
$$



$$
\begin{bmatrix} b_1 \\ b_2 \end{bmatrix} = \begin{bmatrix} 
\cos(30) & \cos(60) \\ 
a_1 \cdot b_2 & a_2 \cdot b_2 \end{bmatrix}
\cdot
\begin{bmatrix} 
a_1 \\ 
a_2 
\end{bmatrix}
$$

Now, let's map a1 onto b2 and a2 onto b2.

$$
a_1 \cdot b_2 = cos(120)
$$

$$
a_2 \cdot b_2 = cos(30)
$$

$$
\left[ \begin{matrix} b_1 \\ b_2 \end {matrix}\right] = \left[\begin{matrix} 
cos(30) & cos(60) \\ 
cos(120) & cos(30) \end{matrix}\right]
\cdot
\left[\begin{matrix} 
a_1 \\ 
a_2 
\end{matrix}\right]
$$

We now have a complete transformation matrix which will allow us to map any vector from the parent frame to the child frame. Now, let's practice translating a vector from the parent frame to the child frame.

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption><p>A vector in the parent frame.</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption><p>The same vector in the child frame.</p></figcaption></figure>

We have a vector in the parent frame with a starting point of (0,0) and an endpoint of (1/2,1/2). Expressed in a matrix this vector is...

$$
\left[\begin{matrix}0.5 \\ 0.5 \end{matrix}\right]
$$

We now want to operate on this vector with our transformation matrix, multiplying the vector by the tranformation matrix.

$$
\left[ \begin{matrix} b_1 \\ b_2 \end {matrix}\right] = \left[\begin{matrix} 
cos(30) & cos(60) \\ 
cos(120) & cos(30) \end{matrix}\right]
\cdot
\left[\begin{matrix} 0.5 \\ 0.5 \end{matrix}\right]
$$

$$
\left[ \begin{matrix} b_1 \\ b_2 \end {matrix}\right] = \left[\begin{matrix} 
cos(30)*0.5 + cos(60)*0.5 \\ 
cos(120)*0.5 + cos(30)*0.5 \end{matrix}\right]
$$

$$
\left[ \begin{matrix} b_1 \\ b_2 \end {matrix}\right] = \left[\begin{matrix} 
0.68 \\ 
0.18 \end{matrix}\right]
$$

We now know how to express the vector V1 from the parent frame, in the child frame.

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

This idea can be extended into 3-dimensions easily.

## A 3-D example

We will now extend this idea of coordinate transformation into 3-dimensions.&#x20;

{% hint style="info" %}
Start with transformation matrix with easy cosine values then backcalculate to label angles between axis using 3-d visualizer. Then just insert snips of 3d image with axis labeled and angles annotated. While I'm making the example image, I should also make several exercise images.
{% endhint %}



## Eigenvalues and Eigenvectors

Very often, in materials science, we are trying to identify transformations of our coordinate axis which eliminate shear stresses and simplify our stress state to one which contains only normal stresses. This coordinate system is often termed the "Principal Axis". This special type of transformation yields a transformation matrix populated by "Eigenvectors". In other words, eigenvectors are the cosines of the angles between the principal axis and the parent axis. When we perform this transformation and eliminate shear stresses, the normal stresses we are left with are called "Eigenvalues". In other words, the eigenvalues are the value of the normal stresses in the special orientation where we have no shear stresses; also known as "Principal Stresses".&#x20;

This is what AI says when asked to explain eigenvectors and eigenvalues and how they are useful in materials science "Eigenvalues are critical values in the context of linear transformations and matrix algebra. They represent the magnitudes of these transformations along specific directions defined by their corresponding eigenvectors. In essence, when a linear transformation is applied to an eigenvector, the resulting vector is simply a scaled version of the original, where the scaling factor is the eigenvalue. This property makes eigenvalues particularly useful in simplifying complex systems, such as stress analysis in materials science, where they correspond to principal stresses in a coordinate system aligned with the principal axes."

