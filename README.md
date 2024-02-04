# clm
clm is a vector and matrix mathematics library written in C. It is designed for 
use in OpenGL projects, much like glm or cglm. Matrices are stored in column major 
representation which aligns with OpenGL's format.

# Usage

Working with Vectors

```c
// Initialise as you would with an array.
clmVec3 vec1 = { 0.0f, 3.0f, -2.0f };
// Or initialise with all zeros.
clmVec3 vec2 = { 0.0f } 

// Scalar multiply vec1 by 5.
clm_v3_scalar_multiply(5.0f, vec1);

// Add v1 and v2 and store the resulting vector in result.
clmVec3 result;
clm_v3_add(v1, v2, result);

// Normalize the result.
clm_v3_normalize(result);

// Get length. (this would return 1 since it was just normalized)
 float len = clm_v3_length(result);
```
Working with Matrices

```c
// Sets transform to be the identity matrix.
clmMat4 transform;
clm_mat4_identity(transform);

// Add a 90 degree rotation to transform around the x axis.
// clm_mat4_rotate expects a unit vector for axis.
float rotation = PI / 2; 
clmVec3 axis = { 1.0f, 0.0f, 0.0f };
clm_mat4_rotate(transform, rotation, axis);

// Add a translation to transform.
clmVec3 translate = { 1.0f, 2.0f, 5.0f };
clm_mat4_translate(transform, translate);

// Send this transform as a model matrix in an OpenGL shader.
unsigned int loc = glGetUniformLocation(shader, "model");
glUniformMatrix4fv(loc, 1, GL_FALSE, transform);
```

Projection and View Matrices

```c
// Create a perspective projection matrix.
clmMat4 proj;
float fov = PI / 4.0f; // 45 degree field of view.
float aspectRatio = 1280.0f / 720.0f; // current screen dimensions.
float near = 0.1f;  // near bound of frustum.
float far = 100.0f; // far bound of frustum.
clm_mat4_perspective(proj, fov, aspectRatio, near, far);

// Create a birds eye view matrix which faces directly downwards towards the 
// origin from above.
clmMat4 view;
clmVec3 position = { 0.0f, 6.0f, 0.0f };
clmVec3 target = { 0.0f, 0.0f, 0.0f };
clmvec3 up = { 0.0f, 1.0f, 0.0f };
clm_mat4_lookat(view, position, target, up);
```

Logging

```c
// To see the values of a vector/matrix in a friendly format.
clm_v3_print(vector);
clm_mat4_print(matrix);
```







