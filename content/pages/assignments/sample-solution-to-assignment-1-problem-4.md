---
content_type: page
description: This section provides a sample solution to Assignment 1, Problem 4.
learning_resource_types:
- Assignments
ocw_type: CourseSection
parent_title: Assignments
parent_type: CourseSection
parent_uid: 1330c237-1da9-2343-e1c5-e39e429984f3
title: Sample Solution to Assignment 1, Problem 4
uid: 3ee3a458-8407-7c89-e496-6206ad4485eb
---

« {{% resource_link 1330c237-1da9-2343-e1c5-e39e429984f3 "Back to Assignments" %}}

/\*

PROG: matrix2

LANG: C

\*/

#include \<stdio.h>

#include \<stdlib.h>

#include \<string.h>

typedef struct Matrix\_s {

 size\_t R, C;

 int \*index;

} Matrix;

Matrix\* allocate\_matrix( size\_t R, size\_t C ) {

 Matrix \*matrix = malloc( sizeof( Matrix ) );

 matrix->R = R;

 matrix->C = C;

 matrix->index = malloc( R \* C \* sizeof( int ) );

 return matrix;

}

void destroy\_matrix( Matrix \*matrix ) {

 free( matrix->index );

 free( matrix );

}

typedef enum {

 REGULAR = 0,

 TRANSPOSE = 1

} Transpose;

// Allowing reading a matrix in as either regular or transposed

Matrix\* read\_matrix( FILE \*input, Transpose orient ) {

 size\_t R, C;

 fscanf( input, "%zu %zu", &R, &C );

 Matrix \*matrix = NULL;

 if( orient == REGULAR ) {

 matrix = allocate\_matrix( R, C );

 for( size\_t r = 0; r \< matrix->R; ++r ) {

 for( size\_t c = 0; c \< matrix->C; ++c ) {

 fscanf( input, "%d", &matrix->index\[c + r \* C\] );

 }

 }

 } else if( orient == TRANSPOSE ) {

 matrix = allocate\_matrix( C, R );

 for( size\_t r = 0; r \< matrix->C; ++r ) {

 for( size\_t c = 0; c \< matrix->R; ++c ) {

 fscanf( input, "%d", &matrix->index\[r + c \* R\] );

 }

 }

 } else {

 fprintf( stderr, "Error: unknown orientation %d.\\n", orient );

 exit( EXIT\_FAILURE );

 }

 return matrix;

}

void print\_matrix( FILE \*output, Matrix \*matrix ) {

 fprintf( output, "%zu %zu\\n", matrix->R, matrix->C );

 for( size\_t r = 0; r \< matrix->R; ++r ) {

 for( size\_t c = 0; c \< matrix->C - 1; ++c ) {

 fprintf( output, "%d ", matrix->index\[c + r \* matrix->C\] );

 }

 fprintf( output, "%d\\n", matrix->index\[matrix->C - 1 + r \* matrix->C\] );

 }

}

Matrix\* product\_matrix( Matrix \*a, Matrix \*b ) {

 if( a->C != b->C ) {

 printf( "Error: tried to multiply (%zux%zu)x(%zux%zu)\\n", a->R, a->C, b->C, b->R );

 exit( EXIT\_FAILURE );

 }

 Matrix \*prod = allocate\_matrix( a->R, b->R );

 size\_t nRows = prod->R, nCols = prod->C, nInner = a->C;

 for( size\_t r = 0; r \< nRows; ++r ) {

 for( size\_t c = 0; c \< nCols; ++c ) {

 prod->index\[c + r \* nCols\] = 0;

 for( size\_t i = 0; i \< nInner; ++i ) {

 prod->index\[c + r \* nCols\] += a->index\[i + r \* nInner\] \* b->index\[i + c \* nInner\];

 }

 }

 }

 return prod;

}

int main(void) {

 FILE \*fin = fopen( "matrix2.in", "r" );

 if( fin == NULL ) {

 printf( "Error: could not open matrix2.in\\n" );

 exit( EXIT\_FAILURE );

 }

 Matrix \*a = read\_matrix( fin, REGULAR );

 Matrix \*b = read\_matrix( fin, TRANSPOSE );

 fclose( fin );

 Matrix \*c = product\_matrix( a, b );

 FILE \*output = fopen( "matrix2.out", "w" );

 if( output == NULL ) {

 printf( "Error: could not open matrix2.out\\n" );

 exit( EXIT\_FAILURE );

 }

 print\_matrix( output, c );

 fclose( output );

 destroy\_matrix( a );

 destroy\_matrix( b );

 destroy\_matrix( c );

 return 0;

}

Below is the output using the test data:

**matrix2:**

 1: OK \[0.006 seconds\]

 2: OK \[0.007 seconds\]

 3: OK \[0.007 seconds\]

 4: OK \[0.019 seconds\]

 5: OK \[0.017 seconds\]

 6: OK \[0.109 seconds\]

 7: OK \[0.178 seconds\]

 8: OK \[0.480 seconds\]

 9: OK \[0.791 seconds\]

10: OK \[1.236 seconds\]

11: OK \[2.088 seconds\]

### « {{% resource_link 1330c237-1da9-2343-e1c5-e39e429984f3 "Back to Assignments" %}}