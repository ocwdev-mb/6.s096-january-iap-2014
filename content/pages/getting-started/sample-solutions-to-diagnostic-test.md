---
content_type: page
description: This section provides sample solutions to select problems from a diagnostic
  test taken by students prior to taking the course.
learning_resource_types: []
ocw_type: CourseSection
parent_title: Getting Started
parent_type: CourseSection
parent_uid: eb6ffd3a-5e1f-1bee-46d8-bbe89130fd37
title: Sample Solutions to Diagnostic Test
uid: f5d748dc-6dd9-6a9a-ab7e-751a2cef2c0b
---

« {{% resource_link eb6ffd3a-5e1f-1bee-46d8-bbe89130fd37 "Back to Getting Started" %}}

The following are sample solutions to problems 8, 9, and 10 of the diagnostic test.

```

/* Notes: as we will be doing in the class, diagnostic.c should be 
compiled with
 * "gcc -std=c99 -m64 -Wall -Wextra -Wshadow -Werror -pedantic"
 * (in particular: we are coding by the C99 standard)
 */
 
#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>
#include <assert.h>
 
/************ PROBLEM 8 ************/
 
bool is_prime( int n ) {
  if( n <= 2 || n % 2 == 0 ) {
    return ( n == 2 );
  }
 
  for( int i = 3; i * i <= n; i += 2 ) {
    if( n % i == 0 ) {
      return false;
    }
  }
 
  return true;
}
 
/************ PROBLEM 9 ************/
 
void swap( int *a, int *b ) {
  int t = *a;
  *a = *b;
  *b = t;
}
 
void permute( int *digits, int n, int p ) {
  if( p == n ) {
    for( int i = 0; i < n; ++i ) {
      printf( "%d ", digits[i] );
    }
    printf( "\n" );
  } else {
    for( int i = p; i < n; ++i ) {
      swap( &digits[p], &digits[i] );
      permute( digits, n, p + 1 );
      swap( &digits[p], &digits[i] );
    }
  }
}
 
void print_permutations( int n ) {
  int *digits = malloc( n * sizeof( int ) );
  for( int i = 0; i < n; ++i ) {
    digits[i] = i + 1;
  }
  permute( digits, n, 0 );
  free( digits );
}
 
/************ PROBLEM 10 ************/
 
size_t search( int *data, size_t N, int value ) {
  for( size_t i = 0; i < N; ++i ) {
    if( data[i] == value ) {
      return i;
    }
  }
  return N;
}
 
size_t binary_search( int *data, size_t N, int value ) {
  size_t lo = 0, hi = N - 1;
 
  while( lo < hi ) {
    size_t mid = lo + ( hi - lo ) / 2;
 
    if( data[mid] < value ) {
      lo = mid + 1;
    } else {
      hi = mid;
    }
  }
 
  return ( hi == lo && data[lo] == value ) ? lo : N;
}
 
/************ TESTING ************/
 
void test_is_prime(void) {
  int N_prime = 10, N_composite = 20;
  int prime[] = { 2, 3, 5, 7, 11, 13, 17, 19, 23, 29 };
  int composite[] = { 1, 4, 6, 8, 9, 10, 12, 14, 15, 16, 
                     18, 20, 21, 22, 24, 25, 26, 27, 28 };
                      
  for( int i = 0; i < N_prime; ++i ) {
    assert( is_prime( prime[i] ) );
  }
 
  for( int i = 0; i < N_composite; ++i ) {
    assert( !is_prime( composite[i] ) );
  }
}
 
void test_print_permutations(void) {
  print_permutations( 3 );
}
 
void test_search(void) {
  size_t N = 7;
  int data[] = { 1, 2, 3, 5, 9, 11, 101 };
 
  assert( search( data, N, 0 ) == 7 );
  assert( search( data, N, 10 ) == 7 );
  assert( search( data, N, 11 ) == 5 );
  assert( search( data, N, 102 ) == 7 );
 
  assert( binary_search( data, N, 0 ) == 7 );
  assert( binary_search( data, N, 10 ) == 7 );
  assert( binary_search( data, N, 11 ) == 5 );
  assert( binary_search( data, N, 102 ) == 7 );
}
 
void run_all_tests(void) {
  test_is_prime();
  test_print_permutations();
  test_search();
}
 
int main(void) {
  run_all_tests();
  return 0;
}
```

_Practices Illustrated_

*   Functions with no parameters are declared with parameter void.
*   We use `size_t` for all array index types that could potentially be large.
*   Judicious horizontal spacing and minimal (but readable) vertical spacing.
*   Curly braces used always (even when optional).
*   Use of the `bool` type from C99's stdbool.h.
*   Variable names are descriptive, but not more verbose than necessary.
*   Each solution to a problem has a piece of code to test it.

« {{% resource_link eb6ffd3a-5e1f-1bee-46d8-bbe89130fd37 "Back to Getting Started" %}}