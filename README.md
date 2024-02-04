# clm
clm is a vector and matrix mathematics library written in C. It is designed for 
use in OpenGL projects, much like glm or cglm. Matrices are stored in column major 
representation which alligns with OpenGL's format.

# Usage

Create a 4x4 identity matrix

```c
// Sets id to be the identity matrix.
clmMat4 id;
clm_mat4_identity(&id);
```

