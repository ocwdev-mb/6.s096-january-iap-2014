---
content_type: page
description: This section provides a sample solution to Assignment 1, Problem 1.
learning_resource_types:
- Assignments
ocw_type: CourseSection
parent_title: Assignments
parent_type: CourseSection
parent_uid: 1330c237-1da9-2343-e1c5-e39e429984f3
title: Sample Solution to Assignment 1, Problem 1
uid: 078c6a84-ee88-3afe-34f2-c31a5dcd5d65
---

« {{% resource_link 1330c237-1da9-2343-e1c5-e39e429984f3 "Back to Assignments" %}}

/\*

PROG: floating

LANG: C

\*/

#include \<stdio.h>

#include \<stdlib.h>

#include \<stdint.h>

#include \<math.h>

#define ABSOLUTE\_WIDTH 31

#define MANTISSA\_WIDTH 23

#define EXPONENT\_WIDTH 8

#define EXPONENT\_MASK 0xffu

#define MANTISSA\_MASK 0x007fffffu

#define EXPONENT\_BIAS 127

union float\_bits {

 float f;

 uint32\_t bits;

};

void print\_float( FILE \*output, float f ) {

 union float\_bits t; t.f = f;

 uint32\_t sign\_bit = ( t.bits >> ABSOLUTE\_WIDTH );

 uint32\_t exponent = ( t.bits >> MANTISSA\_WIDTH ) & EXPONENT\_MASK;

 uint32\_t mantissa = ( t.bits  &  MANTISSA\_MASK );

 if( sign\_bit != 0 ) {

 fprintf( output, "-" );

 }

 if( exponent > 2 \* EXPONENT\_BIAS ) {

 fprintf( output, "Inf\\n" ); /\* Infinity \*/

 return;

 } else if( exponent == 0 ) {

 fprintf( output, "0." ); /\* Zero or Denormal \*/

 exponent = ( mantissa != 0 ) ? exponent + 1 : exponent;

 } else {

 fprintf( output, "1." ); /\* Usual \*/

 }

 for( int k = MANTISSA\_WIDTH - 1; k >= 0; --k ) {

 fprintf( output, "%d", ( mantissa >> k ) & 1 );

 }

 if( exponent != 0 || mantissa != 0 ) {

 fprintf( output, " \* 2^%d\\n", (int) ( exponent - EXPONENT\_BIAS ) );

 }

}

int main() {

 FILE \*input  = fopen( "floating.in",  "r" ),

 \*output = fopen( "floating.out", "w" );

 size\_t N; float f;

 fscanf( input, "%zu", &N );

 for( size\_t i = 0; i \< N; ++i ) {

 fscanf( input, "%f", &f );

 print\_float( output, f );

 }

 fclose( input );

 fclose( output );

 return 0;

}

_Below is the output using the test data:_

**floating:**

 1: OK \[0.004 seconds\] OK!

 2: OK \[0.004 seconds\] OK!

 3: OK \[0.004 seconds\] OK!

 4: OK \[0.004 seconds\] OK!

 5: OK \[0.005 seconds\] OK!

 6: OK \[0.004 seconds\] OK!

 7: OK \[0.004 seconds\] OK!

### « {{% resource_link 1330c237-1da9-2343-e1c5-e39e429984f3 "Back to Assignments" %}}