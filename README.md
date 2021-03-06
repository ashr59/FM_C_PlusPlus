# FM_C_PlusPlus
This package contains a C++ implementation of the <a href="https://en.wikipedia.org/wiki/Fast_marching_method">Fast Marching (FM) integrator</a> for non-convex domains which can probably include some holes. This implementation is used in our paper entitled:
<br>
<br>
<a href="https://link.springer.com/article/10.1007/s41095-016-0075-z"> Fast and accurate surface normal integration on non-rectangular domains</a>.
<br>
<hr>
<br>
Here, I explain the running process by an example:
Our input sample is the *"lena"* image with the resolution of 256\times256.
The program consists of one cpp file (FM2H.cpp) and 4 header files:

```
pix.h
geo_upwind2.h
Marli_heap.h
sobel.h
```

it is better to open all five files in a coding environmeent before running the program 
since you have to change some parameters before starting the process:


First, you have to determine the number of rows in the input image which is the number in front of 
```
# define MAX_X
```
and number of columns in the input image which is the number in front of 
```
# define MAX_Y
```
in these files:
```
FM2H.cpp
geo_upwind2.h
sobel.h
```
Then determine *LAMBDA* value & the *input file name* in the **FM2H.cpp** file.

*(feel free to modify the code to perform them Automatically)*

concerning the mask image, you have to save it with the name of **mask.png**.

if you are intrested to create holes in your mask do it by nested for loops (see FM2H.cpp file line 77 or 82).

Then save all the changes.

Next,you have to be sure about the current path which should be the folder containing the program files.

Then you can build the program with the use of this prompt:
```
g++ `pkg-config opencv --cflags` FM2H.cpp  -o FM2H `pkg-config opencv --libs`
```
then (when you see no error, it is possible to get some warning messages, ignore them!) it is time to run the compiled program by:
```
./FM2H
```
After that you will have the output of the whole program in **result.txt** file.

Now it is time to use the Matlab program **see_result_withmask.m** to see the result and have the *Mean Squared Error (MSE)* rate of the output.

*(you can also here write your own C++ code to avoid using Matlab)*

This program has 3 input parameters:
```
see_result_withmask(filename,N,M)
Filename: is the input file name in string for example: 'lena.png'
N: number of rows in the input image (256 in the case of "lena" image)
M: number of columns in the input image (256 in the case of "lena" image)
```
The result will be saved as the **output.png** file.

In the case of getting **Segmentation Fault Core Dumped** error on a Linux system:
```
1.Login via Linux terminal.
2.Increase the "stack size" by:
$ulimit -s KBytes (65356 should be enough for an image with the size of 1024*1024 pixels).
3.run the program again.
```
In other operating systems you can also solve the core dumpled problem with some efforts. :)


