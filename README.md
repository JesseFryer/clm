# clm
clm is a vector and matrix mathematics library written in C. It is designed for 
use in OpenGL projects, much like glm or cglm. Matrices are stored in column major 
representation which aligns with OpenGL's format.

# Usage

Working with Vectors

```c
// Initialise a vec3.
clmVec3 vec = (clmVec3) { 0.0f, 3.0f, -2.0f };

// Scalar multiply a vec3.
vec = clm_v3_scalar_multiply(5.0f, vec);

// Add two vectors together.
vec = clm_v3_add(vec, (clmVec3) {1.0f, 2.0f, -5.0f});

// Normalize the result.
vec = clm_v3_normalize(vec);

// Get length. (this would return 1 since it was just normalized)
float len = clm_v3_length(vec);
```
Working with Matrices

```c
// Start with an identity matrix.
clmMat4 transform = clm_mat4_identity();

// Add a 90 degree rotation to transform around the x axis.
// clm_mat4_rotate expects a unit vector for axis.
float degrees = CLM_PI / 2; 
clmVec3 axis = { 1.0f, 0.0f, 0.0f };
transform = clm_mat4_rotate(transform, degrees, axis);

// Add a translation to transform.
transform = clm_mat4_translate(transform, (clmVec3) { 1.0f, 2.0f, 5.0f });
```

Projection and View Matrices

```c
// Create a perspective projection matrix.
float fov = CLM_PI / 4.0f; // 45 degree field of view.
float aspectRatio = 1280.0f / 720.0f; // current screen dimensions.
float near = 0.1f;  // near bound of frustum.
float far = 100.0f; // far bound of frustum.
clmMat4 projPerspective = clm_mat4_perspective(fov, aspectRatio, near, far);

// Create an orthographic projection.
float left = 0.0f;
float right = 200.0f;
float bottom = 0.0f;
float top = 200.0f;
float near = 0.1f;
float far = 100.0f;
clmMat4 projOrtho = clm_mat4_ortho(left, right, bottom, top, near, far);

// Create a birds eye view matrix which faces directly downwards towards the 
// origin from above.
clmVec3 position = { 0.0f, 6.0f, 0.0f };
clmVec3 target = { 0.0f, 0.0f, 0.0f };
clmvec3 up = { 0.0f, 1.0f, 0.0f };
clmMat4 view = clm_mat4_lookat(position, target, up);
```
