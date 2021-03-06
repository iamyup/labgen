# LaBGen

![Screenshot](readme/graphical-abstract.png)

LaBGen is a patch-based stationary background generation method that was introduced in [1] and extensively described in a journal paper under review. Note that LaBGen has been ranked first during the [IEEE Scene Background Modeling Contest (SBMC) 2016](http://pione.dinf.usherbrooke.ca/sbmc2016). The purpose of this repository is twofold:

1. To share the source code of the method.
2. To embed the method in a ready-to-use program.

## Compiling the program

The program has been developed in standard C++ and is distributed under the [GPLv3](LICENSE) license. In order to compile it, you need a C++ compiler, a copy of the [Boost](http://www.boost.org) library, a copy of the [OpenCV](http://opencv.org) library, and the [CMake](https://cmake.org) build automation tool. On UNIX-like environments, the program can be compiled as follows, considering that your terminal is in the source code directory:

```
$ cd build
$ cmake -DCMAKE_BUILD_TYPE=Release ..
$ make
```

## Running the program

Once the program has been compiled, the following command gives the complete list of the options:

```
$ ./LaBGen-cli -h
```

In this program, the syntax used to provide the path of the input video sequence is the same one used by the OpenCV library. Thus, for instance, one can generate a stationary background image for the IBMtest2 sequence of the [SBI dataset](http://sbmi2015.na.icar.cnr.it/SBIdataset.html) [3] with *(A, S, N, P) = (MoG Z., 5, 3, 1)* as follows:

```
$ ./LaBGen-cli -i path_to_IBMtest2/IBMtest2_%6d.png -o my_output_path -a mog_zivkovic -s 5 -n 3 -p 1
```

One can directly use the default set of parameters with the `-d` option:

```
$ ./LaBGen-cli -i path_to_IBMtest2/IBMtest2_%6d.png -o my_output_path -d
```

and the universal set of parameters with the `-u` option and a chosen background subtraction algorithm given with the `-a` option:

```
$ ./LaBGen-cli -i path_to_IBMtest2/IBMtest2_%6d.png -o my_output_path -u -a frame_difference
```

The following strings are accepted with the `-a` option: `frame_difference`, `mog_grimson`, `mog_zivkovic`, `pfinder`, `lbp`, `som_adaptive`, `vumeter`, `kde`, `sigma_delta`, `subsense`. Finally, one can observe the processing performed by LaBGen in graphical windows by adding the `-v` option:

```
$ ./LaBGen-cli -i path_to_IBMtest2/IBMtest2_%6d.png -o my_output_path -u -a frame_difference -v
```

With this last option, the processing will be slower has an estimation of the stationary background is generated after each frame in the corresponding window. Here is an example of the execution of the program with the `-v` option:

![Screenshot](readme/screenshot.png)

Note that the program has been successfully tested on Debian-like GNU/Linux operating systems (compiled with `g++`) and macOS (compiled with `clang++`).

## Citation

If you use the LaBGen algorithm in your work, please cite the paper [1].

```
@inproceedings{Laugraud2015Simple,
  title = {Simple median-based method for stationary background generation using background subtraction algorithms},
  author = {B. Laugraud and S. Pi{\'e}rard and M. Braham and M. {Van Droogenbroeck}},
  booktitle = {International Conference on Image Analysis and Processing (ICIAP), Workshop on Scene Background Modeling and Initialization (SBMI)},
  series = {Lecture Notes in Computer Science},
  volume = {9281},
  pages = {477-484},
  year = {2015},
  publisher = {Springer},
  doi = {10.1007/978-3-319-23222-5_58}
}
```

## Acknowledgments

This program incorporates some parts of the [BGSLibrary](https://github.com/andrewssobral/bgslibrary) [2]. We are very grateful to Andrews Sobral for sharing his library.

## References

[1] B. Laugraud, S. Piérard, M. Braham, M. Van Droogenbroeck. Simple median-based method for stationary background generation using background subtraction algorithms. *International Conference on Image Analysis and Processing (ICIAP), Workshop on Scene Background Modeling and Initialization (SBMI)*, 9281:477-484, 2015.

[2] A. Sobral. BGSLibrary: An OpenCV C++ Background Subtraction Library. *Workshop de Visao Computacional (WVC)*, 2013.

[3] L. Maddalena, A. Petrosino. Towards Benchmarking Scene Background Initialization. *International Conference on Image Analysis and Processing Workshops (ICIAP Workshops)*, 9281:469-476, 2015.
