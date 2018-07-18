#AOS vs. SOA: Array of Structures versus Structure of Arrays

struct Quadratic {
	public:
       float a, b, c;
};

our target: calculate the principle root(4ac - b&2/2a) of each and store them in the roots array.

const int count = 1<<24; //suppose we have 16m data
Quadratic* e = new Quadratic[count];
float *roots = new float[count];

//set up random values for all those e

naive way is just to use a loop

however, modern cpus all have SIMD. How we can utilize this?

currently, the data in memory is 

A0, B0, C0, A1, B1, C1, A2, B2, C2, ...

but in the same register, we will have A, B , C... which is not good. The concern here is mainly the locality for caching. 

we want to make all As be together, same to B and C. 

that’s why we would like to have structure of arrays (SOA)

then we can use some SIMD techniques to improve the performance of the computation. 

