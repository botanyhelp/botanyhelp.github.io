## C

Computer science departments still primarily teach Java and/or C.  Java and C take five times longer to learn than python and ruby.  Learning C is best done with these books, in this order:

* The C Programming Language 2nd Edition by Brian W. Kernighan and Dennis M. Ritchie
* Memory as a Programming Concept in C and C++ by Frantisek Franek

### OpenMP programming, compilation, execution, benchmarking in C++ on linux

Some code is shown below that will exercise multicore machinery.  Here we will show the steps used to compile it on linux and run it and see how much faster the OpenMP library can make it with multiple cores.  

We compile the code in laplace2d-omp1-3.cpp **shown below** on linux like this:

```
g++ -fopenmp laplace2d-omp1-3.cpp -o laplace2d-omp1-3
```

We run it like this:

```
./laplace2d-omp1-3 
Solving Laplace equation on 4000-by-4000 mesh.
Using 16 thread(s).
Iteration: 1000, error: 0.372606
Iteration count breached. Error: 0.372606
```

We use the time command and notice that there are probably 16 cores in this machine because 6 minutes and 12 seconds is 372 seconds.  But it only took 23 seconds to run.  **372/23 = 16**:


```
time ./laplace2d-omp1-3 >& laplace2d-omp1-3.log
real	0m23.454s
user	6m12.657s
sys	0m0.079s
```

We can see the output from the execution confirms 16 cores:

```
cat laplace2d-omp1-3.log

Solving Laplace equation on 4000-by-4000 mesh.
Using 16 thread(s).
Iteration: 1000, error: 0.372606
Iteration count breached. Error: 0.372606
```

We can see a nice machine here on linux:

```
cat /proc/cpuinfo |head -25

processor	: 0
vendor_id	: GenuineIntel
cpu family	: 6
model		: 45
model name	: Intel(R) Xeon(R) CPU E5-2670 0 @ 2.60GHz
stepping	: 7
cpu MHz		: 1200.000
cache size	: 20480 KB
physical id	: 0
siblings	: 8
core id		: 0
cpu cores	: 8
apicid		: 0
initial apicid	: 0
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon pebs bts rep_good xtopology nonstop_tsc aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 cx16 xtpr pdcm dca sse4_1 sse4_2 x2apic popcnt aes xsave avx lahf_lm ida arat epb xsaveopt pln pts dts tpr_shadow vnmi flexpriority ept vpid
bogomips	: 5200.05
clflush size	: 64
cache_alignment	: 64
address sizes	: 46 bits physical, 48 bits virtual
power management:
```

And also count 16 physical cores:

```
cat /proc/cpuinfo |grep processor|wc -l
16
```


Thanks for sharing whomever.  I wish I knew and could cite whoever wrote this code:

```cpp
/*  
    Solves the homogeneous (no-source) heat transfer equation
    using 2nd order central finite difference.

    The Laplace equation:   \nabla^2 T = 0   in 2D plane
                                     T = T0  on the plane boundary

    The discretized equation:

       T(i+1,j) + T(i-1,j) - 4*T(i,j) +  T(i,j+1) + T(i,j-1)  = 0   for i=2:M-1, j=2:N-1
       T(1,j) = 1                                           for j=1:N 
       T(M,j) = T(i,1) = T(i,N) = 0                         for j=1:N and i=1:M

    The above system of M*N unknowns and M*N equations will be solved using 
    Jacobi iteration:
 
    1. Start with a guess T
    2. Update Tnew = 1/D ( - R * T)   where D, R are the diagonal and non-diagonal 
       component matrix  corresponding to the linear system above (A = D+R)
    3. Error = || Tnew - T ||, where we use L-2 norm (rms of update)
    4. Check if error < tol, if not go to step-2

*/
#include <iostream>
#include <cmath>
#include <omp.h>
using namespace std;

// set precision by redefining typedef
typedef double real;


int main()
{
   // Set my simulation parameters
   const size_t m = 4000;
   const size_t n = 4000;
   const int iter_max = 1000;
   
   const real tol = 1.0e-2;
   const real rho = 0.25;

   // Allocate
   real T[m][n];
   real Tnew[m][n];

   // Echo the conditions
   cout << "Solving Laplace equation on " << m << "-by-" << n << " mesh.\n"
        << "Using " << omp_get_max_threads() << " thread(s)." << endl;

   // Set Initial guess as zero everywhere except at the west boundary 
   for( int i=0; i<m; ++i )
      for( int j=0; j<n; ++j )
      {
         if ( i == 1 ) T[i][j] = 1;
         else          T[i][j] = 0;
      }

   
   // Start the iterations
   double error = 0; // error is shared/reduced for the parallel region
   int iter = 0;

   // begin the parallel region
   #pragma omp parallel
   {
   while ( true )
   {
      // Reset rms error
      #pragma omp master
      error = 0;
      #pragma omp barrier

      #pragma omp for reduction(+:error)
      for( int i = 1; i < m-1; i++ )
         for( int j = 1; j < n-1; j++)
         {
            //Tnew[i][j] = 0.25 * (T[i+1][j] + T[i-1][j] + T[i][j+1] + T[i][j-1]);
            //121412-dontcopy
            //Tnew[i][j] = 0.25 * (T[i+1][j] + T[i-1][j] + T[i][j+1] + T[i][j-1]);
            //T[i][j] = 0.25 * (Tnew[i+1][j] + Tnew[i-1][j] + Tnew[i][j+1] + Tnew[i][j-1]);
            T[i][j] = 0.25 * (T[i+1][j] + T[i-1][j] + T[i][j+1] + T[i][j-1]);
            double errij = Tnew[i][j] - T[i][j];
            error += errij * errij;
         }
      // normalize rms error
      #pragma omp single
      error = sqrt(error);

      // Check for stopping condition
      if ( error < tol ) {
         #pragma omp master
         cout << "\nTolerance satisfied. Error: " << error << "\n";

         break;
      }
      else if ( iter > iter_max )
      {
         #pragma omp master
         cout << "\nIteration count breached. Error: " << error << "\n";

         break;
      }
      
      // Update guess for next iteration
      #pragma omp for
      for( int i = 1; i < m-1; i++ )
         for( int j = 1; j < n-1; j++)
            T[i][j] = Tnew[i][j];
      
      // display progress every so iterations
      #pragma omp master
      {
      if ( iter % 10 == 0 ) 
         cout << "\rIteration: " << iter << ", error: " << error << flush;
      
      // go to next iteration
      iter++;
      }
   }
   } // end parallel region
   // done
   return 0;
}
```
