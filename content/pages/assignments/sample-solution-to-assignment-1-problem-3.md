---
content_type: page
description: 'This section provides a sample solution to Assignment 1, Problem 3.  '
learning_resource_types:
- Assignments
ocw_type: CourseSection
parent_title: Assignments
parent_type: CourseSection
parent_uid: 1330c237-1da9-2343-e1c5-e39e429984f3
title: Sample Solution to Assignment 1, Problem 3
uid: 91b98c31-93e8-a0ed-1427-bfc4b4f3bd48
---

« {{% resource_link 1330c237-1da9-2343-e1c5-e39e429984f3 "Back to Assignments" %}}

/\*

PROG: matrix

LANG: C

\*/

#include \<stdio.h>

#include \<stdlib.h>

#define MAXN 300

typedef struct Matrix {

 size\_t R, C;

 int index\[MAXN\]\[MAXN\];

} Matrix;

void read\_matrix( FILE \*fin, Matrix \*matrix ) {

 fscanf( fin, "%zu %zu", &matrix->R, &matrix->C );

 if( matrix->R >= MAXN || matrix->C >= MAXN ) {

 printf( "Error: tried to read matrix with a dimension larger than %d\\n", MAXN );

 exit( EXIT\_FAILURE );

 }

 for( size\_t r = 0; r \< matrix->R; ++r ) {

 for( size\_t c = 0; c \< matrix->C; ++c ) {

 fscanf( fin, "%d", &matrix->index\[r\]\[c\] );

 }

 }

}

void print\_matrix( FILE \*fout, Matrix \*matrix ) {

 fprintf( fout, "%zu %zu\\n", matrix->R, matrix->C );

 for( size\_t r = 0; r \< matrix->R; ++r ) {

 for( size\_t c = 0; c \< matrix->C - 1; ++c ) {

 fprintf( fout, "%d ", matrix->index\[r\]\[c\] );

 }

 fprintf( fout, "%d\\n", matrix->index\[r\]\[matrix->C - 1\] );

 }

}

void mult\_matrix( Matrix \*a, Matrix \*b, Matrix \*prod ) {

 if( a->C != b->R ) {

 printf( "Error: tried to multiply (%zux%zu)x(%zux%zu)\\n", a->R, a->C, b->R, b->C );

 exit( EXIT\_FAILURE );

 }

 size\_t inner = a->C;

 prod->R = a->R;

 prod->C = b->C;

 for( size\_t r = 0; r \< prod->R; ++r ) {

 for( size\_t c = 0; c \< prod->C; ++c ) {

 prod->index\[r\]\[c\] = 0;

 for( size\_t i = 0; i \< inner; ++i ) {

 prod->index\[r\]\[c\] += a->index\[r\]\[i\] \* b->index\[i\]\[c\];

 }

 }

 }

}

int main(void) {

 FILE \*fin = fopen( "matrix.in", "r" ),

 \*fout = fopen( "matrix.out", "w" );

 if( fin == NULL ) {

 printf( "Error: could not open matrix.in\\n" );

 exit( EXIT\_FAILURE );

 }

 if( fin == NULL ) {

 printf( "Error: could not open matrix.out\\n" );

 exit( EXIT\_FAILURE );

 }

 Matrix a, b, c;

 read\_matrix( fin, &a );

 read\_matrix( fin, &b );

 fclose( fin );

 mult\_matrix( &a, &b, &c );

 print\_matrix( fout, &c );

 fclose( fout );

 return 0;

}

Below is the output using the test data:

**matrix:**

 1: OK \[0.004 seconds\]

 2: OK \[0.004 seconds\]

 3: OK \[0.004 seconds\]

 4: OK \[0.013 seconds\]

 5: OK \[0.009 seconds\]

 6: OK \[0.006 seconds\]

 7: OK \[0.011 seconds\]

 8: OK \[0.011 seconds\]

 9: OK \[0.012 seconds\]

10: OK \[0.004 seconds\]

### « {{% resource_link 1330c237-1da9-2343-e1c5-e39e429984f3 "Back to Assignments" %}}